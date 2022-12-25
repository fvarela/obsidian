
Downtime:

	SELECT Id,
	Location__r.Name,
	Case__r.CaseNumber,
	CreatedBy.Name,
	Assets__c,
	Duration_in_Minutes__c,
	Downtime_Start__c,
	Downtime_End__c,
	Contractual_Downtime__c,
	Agreed_Downtime__c,
	Work_Order__r.WorkOrderNumber
	FROM Machine_Downtime__c
	WHERE CreatedBy.Name = 'Vern Westervelt'