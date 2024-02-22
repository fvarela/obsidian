index="pt_ntpc" sourcetype="csv_ntpc_subspot" spot_id=P020_1_-1869343515_1_20_272
|sort +bunch_number
| eval x_positions=split(x_position, ";")
| mvexpand x_positions
| streamstats count as sequence by bunch_number
| table bunch_number, x_positions, sequence


index="pt_mcs" sourcetype="csv_mcs_odometers"
|dedup dedup_id
|strcat sn "_" tr sntr
|search sntr IN (*)
|stats sum(GantryRotation) as gantry_degrees min(timestamp) as first_gantry_date, max(timestamp) as last_gantry_date by sntr
| eval start_time_epoch=strptime(first_gantry_date, "%Y-%m-%d %H:%M:%S")
| eval end_time_epoch=strptime(last_gantry_date, "%Y-%m-%d %H:%M:%S")
| eval time_difference_seconds = end_time_epoch - start_time_epoch
| eval gantry_days = round(time_difference_seconds / 86400)
| eval first_gantry_date=substr(first_gantry_date, 1, 10)
| eval last_gantry_date=substr(last_gantry_date, 1, 10)
|eval gantry_degrees = round(gantry_degrees)
|eval full_360_rotations = round(gantry_degrees/360)
|join type=left sntr [
search index="pt_fields"
|dedup irradiation_session_id
|strcat sn "_" tr sntr
|search sntr IN (*)
|stats dc(irradiation_session_id) as total_irradiations, min(timestamp) as first_date, max(timestamp) as last_date by sn, sntr
| eval start_time_epoch=strptime(first_date, "%Y-%m-%d %H:%M:%S")
| eval end_time_epoch=strptime(last_date, "%Y-%m-%d %H:%M:%S")
| eval time_difference_seconds = end_time_epoch - start_time_epoch
| eval first_irradiation_date=substr(first_date, 1, 10)
| eval last_irradiation_date=substr(last_date, 1, 10)
| eval irradiation_days = round(time_difference_seconds / 86400)
| eval irradiations_by_day = round(total_irradiations/irradiation_days,2)
| table sn, sntr, total_irradiations,irradiations_by_day, irradiation_days, first_irradiation_date, last_irradiation_date
]
|eval rotations_per_patient = round(full_360_rotations/total_irradiations,2)
|eval rotations_per_day = round(full_360_rotations/gantry_days,2)
|eval sn = substr(sntr,0,4)
|join type=left sn
[search index="pt_general"
type=hospital_data
|eval long_name = asset.": ".hospital_name
|sort asset
|eval asset = substr(asset,4,10)
|table asset, long_name
|rename long_name as hosp, asset as sn]
|table hosp, sn, sntr , total_irradiations, irradiation_days, first_irradiation_date, last_irradiation_date, full_360_rotations, rotations_per_patient, rotations_per_day, gantry_days, first_gantry_date, last_gantry_date
|rename hosp as "Hospital", sntr as "Serial Number and Treatment Room", total_irradiations as "Total Clinical Irradiations", full_360_rotations as "Full Gantry Rotations (360º)", rotations_per_patient as "Full Gantry Rotations by Clinical Irradiation", rotations_per_day as "Full Rotations by Day", gantry_days as "Gantry Days", first_gantry_date as "First Gantry Date", last_gantry_date as "Last Gantry Date", irradiation_days as "Clinical Irradiation Days", first_irradiation_date as "First Clinical Irradiation Date", last_irradiation_date as "Last Clinical Irradiation Date"






#Avergage patients by site
index="pt_fields"
|dedup irradiation_session_id
|strcat sn "_" tr sntr
|search sntr IN (*)
|stats dc(patient_id) as total_patients, min(timestamp) as first_date, max(timestamp) as last_date by sn
| eval start_time_epoch=strptime(first_date, "%Y-%m-%d %H:%M:%S")
| eval end_time_epoch=strptime(last_date, "%Y-%m-%d %H:%M:%S")
| eval time_difference_seconds = end_time_epoch - start_time_epoch
| eval first_patient_day=substr(first_date, 1, 10)
| eval last_patient_date=substr(last_date, 1, 10)
| eval patient_days = round(time_difference_seconds / 86400)
| eval patients_by_day = round(total_patients/patient_days,2)
| table sn, sntr, total_patients,patients_by_day, patient_days, first_patient_day, last_patient_date
|join type=left sn
[search index="pt_general"
type=hospital_data
|eval long_name = asset.": ".hospital_name
|sort asset
|eval asset = substr(asset,4,10)
|table asset, long_name
|rename long_name as hosp, asset as sn]

#Patients by site, no average:

index="pt_ntpc" sourcetype="csv_ntpc_subspot" spot_id=P020_1_-1869343515_1_20_272
|sort +bunch_number
| eval x_positions=split(x_position, ";")
| mvexpand x_positions
| streamstats count as sequence by spot_id
| chart values(x_positions) by sequence


# Histogramas

* Histograma de una única métrica

```index="pt_ntpc" sourcetype="csv_ntpc_field" flash IN (1)
| stats count by dose_rate_calc_mu_min_mean
 
|bin dose_rate_calc_mu_min_mean as bins span=10000
| stats count by bins
|sort bins
```

* Comparar métricas de flash y non-flash con histogramas:
```
index="pt_ntpc" sourcetype="csv_ntpc_field" flash IN (1, 0)
| eval irradiation_type=case(flash=1, "flash", flash=0, "no_flash") 
| bin dose_rate_calc_mu_min_mean as dose_rate_bin span=2000
| stats count by irradiation_type dose_rate_bin
| eventstats sum(count) as total_count by irradiation_type 
| eval normalized_count = count/total_count 
| chart values(normalized_count) by dose_rate_bin irradiation_type
```