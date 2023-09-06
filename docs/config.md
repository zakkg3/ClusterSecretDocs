# Configuration
 
## replace_exisiting

This enviroment variable is set the behaviour when an existing secret with same same conflicts.
Default is to ignore it and do nothing (to not loose any unintentional data) 
But in some cases we want ClusterSecret to update/reeplace it. In that case set this varaible to 'true'.
