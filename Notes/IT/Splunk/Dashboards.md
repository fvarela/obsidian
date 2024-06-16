## SET TOKENS:

In the begining of the form (just below the <label>):
	<init>
	<unset token="selected_channel"></unset>
	</init>
In an input use <change>  
In a query use:
	<done>
	<progress>
	<finalized>
Set token based on conditions:
	Using IF or CASE
		<change>
		<!--Using IF-->
		<eval token="form.panel">if($time_difference$<=86400,"compare","single")</eval>
		<!--Using CASE-->
		<eval token="showPanelComparison">case($showPanel$=="Comparison","true")</eval>
		</change>
	Using CONDITION:
		<progress>
			<condition match="$master_token$==&quot;Data Entry&quot;">
		</progress>
	Check if token is null:
		<condition match="isnull($arrangements_details$)">
	Check if token is not null:
		<condition match="isnotnull($arrangements_details$)">
	Chek if token has value true:
		<condition match="$arrangements_details$=&quot;true&quot;">

	Using CONDITION on several conditions
		<condition match="'job.resultCount' &gt; 0 AND result.custom_r1p1_vi'==&quot;line&quot;">

Access VALUE, RESULTS and JOB on inputs:
	Access value:
		<change>
			<condition value="compare">
				<set token="showPanelComparison">true</set>
				<eval token="show_interlocks">IF($result$="Machine",1,0)</eval>
			</condition>
		</change>
	Empty value:
		<condition match="isnull($value$)"></condition>
	Search with no results:
		<condition match=" 'job.resultCount' != 0">
	Unset values from a form. Use both tokens below:
		<unset token="selected_channel"></unset>
		<unset token="form.selected_channel"></unset>
	
	Set token after a search:
		<search>
			<query></query>
			<done>
				<condition match=" 'job.resultCount' > 0">
					<set token="label">$result.fileName$</set>
				</condition>
			</done>
		</search>

Set a token after a search based on like value (not regex):
<done>
  <condition match="like($result.all_axes$,&quot;gantry&quot;)">
    <set token="gantry_details">True Value</set>
  </condition>
  <condition>
    <set token="gantry_details">Default Value</set>
  </condition>
</done>
	
## Dashboards


Setting two token off one dropdown
<input type="dropdown" token="application" searchWhenChanged="true">
 ...
 ...
         <change>
               <set token="ip">([subsearch stuff | where application="$value$" | return 1000 IP_Address])</set>
         </change>
 </input>



Conditionally formatting a dashboard:
<format type="color">
          <colorPalette type="expression">if(match(value,"Missing=Yes"),"#53A051",null)</colorPalette>
</format>


 <format type="color" field="date_hour">
          <colorPalette type="expression">case (match(value,"ERROR"), "#DC4E41",match(value,"WARN"), "#F8BE34",match(value,"INFO"),"#53A051",true(),"#C3CBD4")</colorPalette>
        </format>


Encode special characters:
	&lt;  <
	&gt; >
	&amp;  &
	&quot;  "
Alternativa. Encapsularlo todo en <![CDATA[   ....  ]]>:
```
<![CDATA[
      | savedsearch "Mysearch" | where isnotnull(Resource) | rex "r> (\[.*\] )*(?<Reason>.*)$" | fields host,hostname,Resource,Reason
    ]]>
```




Drilldown

            <set token="show_jobs"></set>
            <set token="definition_id">$row.Deployment Name$</set>

	Celda: Primero habilitas el drilldown con esta opción como child de la tabla:
	<option name="drilldown">cell</option>
	Después poner la acción que quieres que se ejecute. También como child de la tabla:
		Enlace a otro dashboard:
		<drilldown>
	          <link target="_blank">/app/search/vida_protons_logs_explorer?form.field1.earliest=$field1.earliest$</link>
	     </drilldown>
	     Poner un token:
	    <drilldown>
          <set token="axis">$click.name2$</set>
        </drilldown>

	Por columna.
		Para hacer un drilldown que ejecute algo cuando se hace click en una celda que está bajo la columna 'component':
```
<drilldown>
          <condition match="$click.name2$==&quot;component&quot;">
					<set token...></set>
			</condition>
</drilldown>
```
	Capturar el valor de un field 'sno' presente en la  fila:
```
<drilldown>
          <condition match="$row.sno$==&quot;2&quot;">
					<set token...></set>
			</condition>
</drilldown>
```
```
	Capturar el valor clickado:
```
<condition match="$click.name2$==&quot;work_orders&quot; AND $click.value2$&gt;0">
	<set token="case_id">$row.case_id$</set>
    <set token="show_work_order"></set>
</condition>
```
Para las celdas en las que no quieras especificar un drilldown pon lo siguiente:
```
     <condition>
          <!-- NO DRILLDOWN FOR OTHER FIELDS -->
     </condition>
```




Convenciones:
El color que uso para los enlaces dentro de una tabla es: #F5FFFA
https://varian.splunkcloud.com/en-US/app/VIDA_Protons/vida_proton_continuous_kv_imaging



Check token status snippet:
  <row>
    <panel>
    <html>
      <div id="tokeninfo">
        <p></p>
      </div>
    </html>
    </panel>
  </row>