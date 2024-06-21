# Load item data Workflow Process 

There are two ways calls extractor api. 1) Calls workflow using cron-job and 2) Calls workflow using kie-server api

# Calls workflow using cron-job
	The load item data process will run the following API through BPM cron job
		
	| Service Endpoint            | Schedule         |
	|:----------------------------|:-----------------|
	| /api/pipeline/trigger       | Every 30 minutes |
	
	Note: Scheduling interval time yet to be decided
	
	Once deployed load-item-data-cron-job workflow on Kie-server, then BPM asset will start to call/run above api

# Calls workflow using kie-server api 
    It can be accessed through below Kie-server REST API. We can test this API using below payload. 
    
# URI: 
    http://<ip>/kie-server/services/rest/server/containers/{MyContainer}/processes/{ProcessId}/instances
# Method: 
    POST
# Path Param: 
    You need to pass deployed container id in {MyContainer} placeholder
    And Each container can have n number of workflow processes. Each workflow has unique process id 
    To call appropriate workflow process, need to pass process id in {ProcessId} placeholder
    Example: in our case deployed container id is 'item-master-data-process_1.0.0' and process id is 'itemMasterDataProcess', so
    http://<ip>/kie-server/services/rest/server/containers/item-master-data-process_1.0.0/processes/itemMasterDataProcess/instances
# Headers: 
    Content-Type: application/json
    Authorization: Basic ************

# Request Payload:       
	{
	    "key": "t_ingram_dataverse_item_source",
	    "message": "Run Item Data Load",
	    "status": "Created",
	    "created_date": "2024-05-11T03:48:14.408273",
	    "processId": 51
	}    

# Response Payload:
    2