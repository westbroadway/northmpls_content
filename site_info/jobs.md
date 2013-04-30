# Jobs

## Feed Sources
* Indeed jobs 55411 and 55410 are fed into the search index every 10 minutes. The TTL on the search index is 8 hours. A ruby worker is called every 10 minutes to pull in the updates.
  * [55411 Feed](http://indeed.herokuapp.com/indeed/55411) `http://indeed.herokuapp.com/indeed/55411`
  * [55412 Feed](http://indeed.herokuapp.com/indeed/55412) `http://indeed.herokuapp.com/indeed/55412`
* Wufoo job submissions are fed into the search index as they are created. If they are edited in wufoo they must manually be updated. The TTL on the search index is 1 year. A webscript.io webhook is called from wufoo on new form submission. Manual updates are triggered using the "full update" button.
  * http://insert.webscript.io/jobs?form_code=z7p6z1&field_map=address1:Field9,address2:Field10,city:Field11,state:Field12,zipcode:Field13,country:Field14,company:Field1,date:DateCreated,jobkey:EntryId,jobtitle:Field5,company_url:Field2,jobtype:Field6,fulltext:Field7,name_first:Field17,name_last:Field18,contact_email:Field20,contact_phone:Field19,compensation:Field8


## User submitted Jobs
* List Name: jobs_northmpls
* Source: search:jobs/submitted (northmpls.org job form submissions added from Wufoo.)
* Feed filter: source:northmpls
* Final filter: approved

## Indeed Jobs
* List Name: jobs_indeed
* Source: search:jobs/indeed (indeed.com jobs)
* Feed filter: zipcode:55411 OR zipcode:55412
* Final filter: not_removed

## Live NorthMPLS.org Job Board
* List Name: jobs_board
* Source: list:jobs_indeed:final AND list:jobs_northmpls:final
* Sort: Created date descending. Newest jobs at the top.

## Example iframe
    <iframe src="http://jobs.northmpls.org" allowTransparency="true" frameborder="0" scrolling="no" style="border:none; overflow:hidden; width:950px; height: 3000px; display: block; margin: 0 auto;></iframe>
