# awscertprep
# AWS Certification Preperation
# AWS Certified SA Professional 

* Cloudwatch

#matrics
Provided by many services.
EC2 standard monitoring- 5 mins, detailed monitoring: 1 min - CPU /network/ram is not there - use custom metrics
custom metric - create by yourself 1- min standard || - 1 sec - high resolution

#Clouwatch Alarms
can trigger actions :
	- EC2 action : reboot /stop /terminate /recover 
	- autoscaling 
	- SNS
Alarm events can be intercepted by CW events.

# Dashboards
- Display matrix and alarms
- can show matrics of multiple regions

# Integrations - 
CW -- ec2 action --> status check ->> recover
CW -- autoscaling 
cw -- sns / fanout/ sqs - lambda
CW alarm - CW events -> kinisis / step function / lambda function 

# Cloudwatch Events-
intercepted events  from AWS services
EX: instance start / code build fails/s3 / TA
Can interceptedd any	API calls with cloud watch integrations

cw events - > target
targets: 
Compute - lambda./ batch job/ ecs task / faget container
orchestraions - pipelien
integration - sqs sns kinisis
Maintainence - SSM Ec2 action	

#CW Logs 
How to get data - SDK , cw logs agent / cw unified agent
Interations: Elastic beanstalk collects logs and send to cw logs
ECS container logs
AWS lambda- 
VPC flow logs
cloudtrail
Api gateway
CW logs agent - installed to ec2/ vms on prepm
Route53 dns logs

- Log groups --> log streams --> logs
Log expiration policies
Encrypt logs wit KMS
Send logs to - s3- (EXPORTS)
kinisis data streams
kinisis data firehose
Elasticsearch
Lambda

Metric filters and filter expression
-- eg specific ip in logs
-- number of occerences of word error
MF used to trigger alarms

Cloudwatch logs insights where you can see and query logs

CW logs --> S3 (Encrypted to AES256)/sse s3 only -- log data takes 12 hr to available -- CreateExportTask -- not real tim
Real time -- use Logs subscription 

Cloudwatch log subscription:: 
Logs --> subscription filter:
	- managed lambda function --> ES (Real time)
	- Kinesis data firehose --> ES // S3  (near real time)
	- Kinesis data stream -- KDF/KDA/EC2/lambda
	
Multi account multi region log aggregation ::
CW logs --> subscription filter ->> ||| -->> kinesis data streams --> firehose --> s3
	
	
Cloudwatch logs angent vs unified agent
With cloudwatch log agent we can send only to cw logs and it is old version
With unified agent send logs to cw logs also metrics such as ram and process and can have central config in ssm peramater store

Batch send:
batch_count -- default 1000 -- min == 1
batch_duration -- default and min 5000ms
batch_size: max size of log - default max 1mb

Both agent cannot send to Kinesis -- for this you need to use kinesis agent insted



XRAY
--Visual analysis of application and tracing capabilities
latency / err rates
Trace request across microservices -- integrations 
EC2 -- install the xray agent .
ECS -- install agent or use xray docker
Lambda 
Beanstalk -- automatic install available
Api gateway -- helpful for errors

Extra agents

-- New section 
## Cost allocation tags
We can enable detailed costing reports
Just like tags but they show up as a coloumn in reports

2 types -- AWS generated CA tags - automatic applied -- aws:createdBy -- not applied to resources that re previously created
User tags - prefix defined by user (user:xxx)

Just appeare in billing console
Takes upto 24 hrs for the tags to show up in report


Tag Editer
-- manage tag for multiple resouces at once
add/update/delete tags
search for tagged and untagged resources

Trusted advisor
High level assistment of account 
analise and provide recomendations
Cost optimization
Performace
Security
Fault tolerance
Service limits

Core checks and recommendation
YOu have access to more checks as per subscription
Can enable weekly notification from console

FUll TA available for business and enterprise support plans
- programatic access / set cw alarms on limits

Support plans
basic - developer - Business - enterprise

TA can check s3 bucket public but cannot check s3 objects public -- for this cw events / s3 events/ insted

Service limits -- cases manually created
For monitoring SL you need business of enterprise plan
API Cannot change limits 

for this
AWS Service quotas is a new service and has an API
 
#Ec2 Cost savings
Ec2 launch types --
Ondemand -- short workload
Spot -- cheap - short workloads
Reserved -- 1 yr - 
convertable reserved
Dedicated instances -- no hardware share
Dedicated host -- your instance placement book a server
	Host affinity -- instence reboot on same host
	Great for software licences that operate at core level

Savings plan
	New pricing model -- wil replace reserved instances
	EC2 instance savings plan -- 72% 
		Commit to a certen type of usage like 10 usd /houe for 1 yr -- above that on demand prices will apply
		can select any family
		can select any os / tenency /size
	Compute savings plan -- 66% same as convertable RI
		move btn family / region/ compute type os and tenancy --ec2 farget lambda
	Sage maker savings plan -- 64% on sagemaker
	
	
S3 Cost savings:
S3 storage class- S3 standerd GP - S3 standaerdIA
One zone IA, Intelligent tiering, Glacier Instent Retrival
Glacier Flexible retrieval, Deep archive

S3 lifecycle configurations

1. S3 select and glacier select.
2. Sr lifecycle rule
3. compress objects
4. S3 Requester pays-- Requestser will pay the download cost / network - S3 bucket policies - auth via iam - assumed cross account role

Budgets --
Usage - cost - reservation - savings plan

RI utilization 

5 sns notification per budget

filter by service , linedaccount, region , az , api etc

First 2 budget are free

Cost Explorer:
Visalize understand and manager data ,
monthly. hrly resource level
Choose optiaml plan
Create custom reports
forcast usage feature 12 months


Other services
Cloud search
Alexa for business ,lex connect	
AWS workspaces - managed VDI , secure cloud desktop-- secure- Microsoft AD - 
	Workspaces application manager - cotainarize apps - deploy an manage, procision scale, keep updated , 
	Windows updates - by default workspaces are configured to  install software updates 
	Maintainance windows
		always on workspaces
		auto stop workspaces
		manual maintainence
App stream 2.0 
	Desktop application streaming service
	The app is dilivered from within web browser
	
The mechnical Turk
	Crowdsourcing marketplace to perform simple human task
	Distributed virtual workforce --  Integrated with SWF but not not with SF
	Like - restaurant name is not perfect - humans will go and check update your database - they get paid
	Data collection / business processing
	
AWS Device Farm
	Running big application --> test with many devices ?
	Test run across real browsers and real mobile devices.
	Fully automates - improve quality - generate automated vids and logs - remotely logun to devices for logging
	
Amazon macie
	Fully managed data security / privicy service that uses machine learning and pattern matching to discovr and protect your sensative data
	Alert you around PII data --> s3 buckets - macie - event bridge - sns / lambda

Amazon transcribe
	Convert - speech to text - deep learing - customer service- gernerate matadata

Amazon workdocs
	Secure content management system - Google drive / one drive /etc
	Access through apis from external customer apps 
	Historical data
	Create store and sync files from any location 
	Encryption R and T
	Workdocs drive
	Approval workflows
	
CICD
		CI
			Build -	
			Jenkins
		CD
			DEPLOY
			Code deploy
			Jenkin
			Spinnaker
	Code - build - test - deploy - provision
	------------------------------------------------------Code Pipeline-----------------------------------------------
	Code commit / github -> Code build / jenkins CI (Build and test)--> AWS Code deploy ->  Beanstalk / ec2 fleet/ lambdas/ 	
	--------------
To help you remember them quickly before going into the exam

CodeCommit: store code in version-controlled repositories. Code can live on multiple branches

CodeBuild: build & test code on-demand in your CICD pipelines.

CodeDeploy: deploy code on EC2, ASG, Lambda or ECS

CodePipeline: orchestrate CICD pipelines. If using CodeCommit as a source, matches to only one branch

CloudSearch: managed search solution to perform a full-text search, auto-completion in your applications

Alexa for Business: use Alexa to help employees be more productive in meeting rooms and their desk

Lex: Automatic Speech Recognition (ASR) to convert speech to text. Helpful to build chatbots

Connect: receive calls, create contact flows, cloud-based virtual contact center

Rekognition: find objects, people, text, scenes in images and videos using Machine Learning

Kinesis Video Stream: one stream per video device, analyze using EC2 instances or Rekognition

WorkSpaces: on-demand Windows workstations. WAM is used to manage applications

AppStream 2.0: stream desktop applications into web browsers

Mechanical Turk: Crowdsourcing marketplace to perform simple human tasks, integration with SWF

Device Farm: Application testing service for your mobile and web applications across real devices


Cloud Front ->
	Content delivery network - improve the read performance - 300+ edge points globally
	Ddos protection - integration with shield, WAF  - Filter request at the edge
	Can expose https and talk to internal https backends
	
	Origins :
		- S3 buckets -> For distributing files , enhance security with cloudfront OAI 
		- Can be used as ingress - allows you to upload file to s3
		- S3 buckets as websites -> enable static website hosting
		- Media storage containers - Media Package endpoints 
			VOD(video on demand) - live streaming vid using aws media services
		- Custom origin - http
			Ec2, ELB , Api gateway , Any HTTP backend, on prem instances
	
	With s3 origin - traffic goes via internal network
	with ec2 / custom htto - traffic goes via internat - need to whitelist all edge location public ip to security group
	With ALB it must be public - allow public ip of edge location to ALB SG -> now ec2 will be private subnets , all SG of alb to EC2
	
	Cloudfront vs S3 Cross region replication 
	CF -
		Global network cdn , files cached, TTl , Static contant, low latency
	CRR -
		Setup for each region ,Files will update near real time, Read only , Active-active Repl, Great for dynamic content 
	
	Cloud front Geo Restriction :
		Allow list - list of allowed contries
		Block list - prevent users/ contries 
		Geo IP database - 3rd party for determining the contry from IP- USecase is copyright content
	
	Cloudfront signed URL - special url to get access to contents of cloudfront - url expires,
		- Create special application server responsible to create signed url
		- client >> application server >> cloudfront << Return url to client --- url >> CF
	Custom origns - ristrict access to ALB
		 1. Application logic : add custom hedder and respond only if that headder is present in the request -header name and value will be secret and cloudfront will add it at time of request
		 2. Filter by || whitlist only cloudfront IP addresses available out there
	
	Cloudfront Caching:
	-Cache based on 
		Header
		Session Cookie
		Query string parameters
	Cache lives in CF edge location
	Maximize the cache hit rate- TTL 0 sec to 1Yr (Cache control header OR the Expires Header)
		Host / user-agent/ Authorization / date /keep-alive / Accepy-ranges -- we need to choose good header
		Like: Authorization and Host which will less change
		-- OR Seperate the static and dynamic layer	form your cf (2 CF distribution 1 wll have s3 origin and other is alb)
	
	CF caching and API gateway caching :
		Api gateway edge mode --> 
		Api gateway regional cache --> Full control on CFD -- (2 cache we will get)

	Customizaton at the edge:
	Run custom logic at the edge
		Edge function - earlly logic - preprocessing
			Code you can wirte and attach to CFD - less letencey - no cache - change request /response
			1. Cloudfront functions 2.Lambda at edge (Regional)
			Use cases : manupulate request /responce , request filtering , auth  and authzn , Generate Http response, bot mitigation (Serverless)
			
		Lambda will be deployed to edge cache- CF funtions will be deployed at the edge location
		CF Functions will interact viewer request and response... Client - cloudfront - Written in JS / High scale latency, sensative, Handel Millions request per sec
			Process based isolation - Cannot call external function /just prefom transformations
		Lambda@edge - Nodejs /py/ scale to 1000rq per sec , vm based isolation/ change viewer and origin request and responses - you need to create in one region then CF will replicate

Http configuration and Host:
	client > CF > ALB -- dont fwd the host header
	Send header if you use same certificates

Elaticache
	Reduce load - load - less query - stateless - session storage - managed service - 
	Using elasticache can have heavy code changes 
	Redis: Multi az - auto failover - Read replicas - HA , persistence / backup and restore
	Memcache: Multi node - partitioning - sharding , non persistent , no backup and restore , multithreaded
	
	- Can be used as DB cache - Lazy loading , hot keys , less load on rds , choose better ttl
	- User session store - (if you have not enable stickiness on alb) -- Statelessness
	
	Limits:
		Handel Extreamly high rates 
		client -> Route53
				> Cloudfront ->  ALB/API gateway  >  ASG/ECS(Slow/ time to scale) > RDS,Aurora, ES (Provisioned)
												  >  Ec2/ Farget (Faster)		  > Dynamo  (Autoscaling , ondemand)
												  > Lambda -- 1000 Concurrent     > Redis -<200 nodes (Replica+sharding)
																				  > Memcache 20 nodes , DAX 10 nodes (p+r)
																				  -> EBS -16k Iops gp2 / 64k iops(io1)
																				  -> Instance store- ms IOPS (Can be used as local cache)
																				  -> EFS - General and MAX Io
																				  
																				  -->SNS SQS (Unltd space)
																				  -->SQS fifo 3000rps 
																				  -->Kinesis 1mbps I and 2mpbs O (Provisioned)
																				  
				>Edge															  S3 --3500 Puts and 5550 Gets /prefix /s
																				  Kms -- limited if encrypted 
																				  
 		CACHE	CACHE			   /10000Rps
			

 
Dynamo DB:
Fully managed : No sql 1,000,000 rps - similar toapache casserndra - no disc space to provision
Max object size is 400kb (WCU RCU) -autoscaling provisioned | On demand
CRUd - Read / eventually -or- Strongly consistent - support transaction across multiple tables(ACID)
Backup support - 2 table classes Standard and Infrequent access IA 
Made of tables - Each table have PK - row and attributes
Data type - string , binary , boolean , null ,number 
Document type - List, map 
Set - string set , number set and binary set

(Primary key)->>Partition key and Partitionkey + sort key(range key)

Indexes: 
	Object = primaryKey + sort key + attributes 
	LSI: keep same primary key + alternative sort key :: Must be defined at table creation time
	GSI: change primary key + optional sort key : can be defined after table creation
TTL for row
Dynamo db streams: React to changes to dynamodb table in real time --> lambda/ec2 , 23 hr of retention in stream
Global tables: Cross region replication Active-active(Must enable DynamoStreams first), low latency, DR, low rto

Kinesis data stream + dynamo db stream :: dynamo>curd>ddbstram>kinesisstream>firehose>sns/lambda/s3/redshift or kinesis analytics
DAX: seamless cache- no application rewrites- Writes go through dax to dynamodb, Micro second latency for cached reads
	Solves hot keys problem : row readed many times-> throttling - default ttl 5 min, utpto 10 nodes , 3 nodes min for production
	Multi az, secure, kms ,iam , cloudtrail, vpc
	DAX vs elasticache what to use? EC for heavy computation and store - Dax for direct reads writes
	
Opensearch:
	Elasticsearch - Kibaana > opensearch dashboards
	Managed ,Needs servers, Log analytics, Real time monitoring, security analytics, indexing , full text serach 
	ELK - on aws 
RDS:
	 Postgre,mysql,maria,oracle,microsoft sql server
	 Managed db:provisioning, backups ,patching and monitoring
	 RDS vpc private subnet- using sgs 
	 if lambda>rds so launch lambda in private vpc
	 Storage By ebs - gp2 /io1 can increase the volume size with autoscaling
	 Backups:automated
	 Snapshots: manual, can make copies of snapshots cross region
	 RDS events: Notify via sns events
	 RDS multi az- standby instance in case of failover -sync-
	 Read replicas - can be cross region - async 
	 
	Security: Kms is there for EBS and snapshots
	TDE for oracle and sql server
	SSL to rds in flight calls for all db
	IAM for my sql and postgresql
	For other - authorization still happens
	Creaate encrypted snapshot from unencrypted rds
	Cloudtrail cannot be used to see queries
	
	R53 health checks are not available for rds use application proxy

RDS for oracle:
	Backups:
		RDS backups - uses rds backup and restore  
		Oracle RMAN - Recovery manager to non rds 
		RDS oracle > ORMAN > S3 > oracle db external
		
	RDS for oracle does not support RAC -- Real application clusters
	RAC is on oracle with ec2
	Supports TDE
	Support DMS - Onpremp oracle >> migrate<AWS DMS> >> Rds oracle
	
RDS for MYsql
	mysqldump - Migrate Mysql rds to non mysql rds (Replication)

RDS proxy to aws lambda:
	Opne and maintain DB connection , many lambda function "TooManyCOnnectionsException"-- RDS proxy
	No need to maintain code for connection cleaning
	Supports IAM auth / db auth / autoscale
	
Cross region failover -- RDS

AUAROA::
	MAZ size is 64 TB
	DB engiens: Postgre sql compatible & My sql compatible
	Storage automatically Grows by increament of 10 gbs to 128 TBs , 6 copies of data, multi az
	ReadReplicas - 15 and get reader endpoints.
	Cross region read replicas. entires database is copied not specific table
	Load/ offload data to/from s3 directly
	Backup snapshot and Restore features same as RDS
	Highly available - 6 copies - 4 for writes and 3 for reads, self healing , peer to peer replication
	Storage is striped in 100s of volumes so no single point of failure.
	
	Aurora serverless : Automated database and autoscaling, good for infrequent / unpridictable workloads.
		No capacity planning / pay per second.
	
	Global aurora: 1 primary region and upto 5 read only region, 16 read replicas/ secondary region , we can pramotoe in dr and rto is < 1 min
	
	Aurora multi master -
		multiple writers , every aurora node can read and write , no need to promote
	Aurora endpoints:
		Endpoint = host address + port
		Cluster endpoint -IUD-query
		Reader endpoint - read/queries
		Custom endpoints - Represent a set on DB instances that you choose (Connect subset of cluster)
		Instance endpoint - connect to specific node
	Logs : Error, slow query , general, audit -- Download or publish to cw
	
	
Service Communications:
Step functions:
	Build serverless visual workflow orchestrate lambda function 
	Flow as a json state machine - sequence - action - parallel actions - condition - timeout, error handeling
	Max execution of a function is 1 Year
	Add human approval functions. If you chain lambda function use sf keep latency in mind
	Integrations:
		Can invoke lambda functions,Run aws batch jobs , run ecs tasks, insert item to dynamo Publish msgs to sns,sqs
		Launch emr jobs, Glue , sagemaker , Launch another stepfunction ++ 200 services with sdk
	Trigger:
		management console, sdk , cli, lambda , api gateway, event bridge, codepipeline, sf
	Tasks:
		Lambda tasks: Invoke lambda
		Activity tasks: Http , ec2, mobile, onprem. Poll step function
		Service tasks: Connect to aws service ,ecs, dynamo, sqs, sns, batch
		Wait task -- wait for duration
	Not integrate with aws mechnical turk
	
SWF: Coordinate work amuong applications, code runs on ec2 ,1 yr, Activity step and decision step.
	Has built in human intervation 
	Eg: order fullfilment.
	External process, child  process return to parant service - Amazon Mechnical truk
	
SQS: Serverless , managed queue, Integrated with IAM, can handel extreame scale, decouple
	Max msg - 256kb, use pointer for large msg - s3
	Can be read from ec2, aws lambda
	SQS - write buffer of dynamo - because of throttling
	FIFO - in order,300msgs /sec , 3000 /s with batching
	Idempotent : to consumer level, Delete msg after processing
	SQS -> event source mapper -> Lambda function
	SQS visibility timeout should be 6x of lambda function 
	DLQ set up at queue level OR lambda destinations
	
Amazon MQ: MQTT/APQP/STOMP - migration , managed active mq. Provisioned, runs on dedicated machine, does not scale, can run in HA mode
	Has SQS and SNS features
	IBM mq, apache mq,tibco ems,active mq can be migrated

SNS: One msg and many receivers - email/queue/mobile/http/lambda/firehose endpoint (Pub sub)
	The 12,500,000 subscriptions/topic -- 100000 topics
	SNS recieve data from cw alarms/budgets/asg/cf/ sr/dns/lambda/d db
	use topic publish api -- direct publish for mobile -
	Security, In flight encryption,at rest, client side encrpn, Access control - Iam policies, Sns access polices(useful fro cross account sns)
	
	SNS SQS + fan out: Fully decoupled, can add more sqs over time, check sqs polices,
		SNS also have fifo, Ordering /fifo
		SNS fifo - > SQS fifo 
		Msg filtering in sns- Add filter policy to subscriptions
		

AWS Kinesis:
	Managed data stream that can ingest lot of data at scale in real time
	Application logs, iot sensor data, matrix,-- Real time big data
	Stream processing - spark, Replicate across 3 az sync
	
	Kinesis streams : Low latency streaming ingestion
	Kinesis Analytics : Perform real time analytics on streams using SQL
	Kinesis Firehose: Load streams into s3 , redshift , ES and splunk
	
	Streams:
		Divided into shards(partitions) Producers and consumers
		24 hr data retention by default - 356 (**7) days
		Abiity to reprocess/replay data, Multiple applications can consume the same stream, Real time, Once you push data,it cannot be deleted. Immutable
		Capacity modes: 1. On demand, Provisioned:You can manage the shards over time
		Baching is also available, resharding/merging
		Records are ordered per shard 
		Producer: AWS SDK, KPL (batch,compression,retries,cpp,java), Kinesis agents(Write to streams and firehose)
		Consumer: AWS SDK, Lambda, KCL(Paralell read, coordinated reads)
		Limits: Producer 1Mbps or 1000 msgs writes /shard - ProvisionedThrughputException, add more shards
		Consumer : 2mbp at read per shard across all consumer, 5 api calls per second per shard across all consumers.
		Consumer enhanced fan out : 2mbps per shard / enhanced consumer - no api needed, push model.
		
	Firehose:
		Take data from producer,like all producer to streams,streams, cw logs ,iot.
		Transform data using lambda(optional)
		Return the data in batches -> AWS(S3,Redshift(Copy from S3),Amazon ES)
								-> 3rd party(Splunk, datadog, mongo,nuwrelic,splunk)
								-> Custom Destination (Http destination)
								-> S3 All failed data / Backup data
		Fully managed, Serverless, autoscaling - Pay for data go through firehose, Near real time- 60 sec latency
		Support many data format- conversion , transformation , or you can write custom transformation usging lambda
		Buffer sizing : Buffer will be fulshed on time and size.
		Firehose can autometically increase the buffer size to increase throughput
		High throughput > Buffer size will hit,
		Low throughput > Buffer time will hit, Need real time flush? Use lambda insted firehose
		
	Analytics:
		Perform computation on stream data - can read from streams and firehose -> Refrence table -> query -> output stream , error stream
		Use case: Striming etl , live leader board , Contineous metric generation, Responsive analytics
		Pay for use not cheap, Iam roles to access streams and destinations, SQLor flink to write computation , Schema discovery, Lambda for preprocessing 
		
	Streaming Architecture:
		Data enginering pipeline:
		
		producer -> KDS -> KDA -> KDS -> EC2
						-> Lambda
						-> KDF ->S3 -> Redshift
									  ->ES
		producer -> KDF -> S3/KDA
		
	3000msgs of 1kb/sec
		KDS -> Lambda (Cheaper)
		Dynamo -> Lambda (Costly)
	
AWS Batch:
	Run batch jobs as docker images:
	Run on aws fargate (Fully serverlss)
	Dynamic provisioning of the instances Ec2 - spot instances in vpc
	No need to manage / fully serverless
	Batch of images /thousand of concurrent jobs/ schedule batch jobs / orchrestrate using SF
	
	Lambda: time limit - limited runtime - special docker images- temp space- serverless
	Batch : No time limit, any docker image, relie on ebs or fargate or ec2, any runtime
	
	Compute env:
		 Managed compute env
			AWS batch managed the capacity and instance types
			You can choose on demand or spot
			Set max prize
			launch in own vpc -- private subnet must have access to ecs , Nat gateway or vpc endpoint to ecs serivuce
		
			Batch , min max cpu, spot , Batch jobs quque, sdk-> add jobs > jobs quque . Can use autoscaling on job queue.
			Multi node mode: large scale HPC, multiple ec2/ ecs  at same time to share the workload, Single jobs run on many node, main node and child node(not for spot) works better with cluster placement group
			
	
		Unmanaged:
EMR:
	Elastic map reduce/ big data / hadoop clusters
	Use emr when migration -> jobs, 100s of ec2 , launch in bigdata ecosystem, apache, spark , hbase , presto
	EMR takes care for confg and provisioning, autosacling with cloudwatch
	
	Integrations:
		Launch in VPC, single AZ, EBS (for HDFS)- temporary storage
		Use EMRFS native integration with s3 for permanenet storage , SSE
		Run apache hive on your data -> Read from dynamo db table
	Optimize cost:
		Master node : manage
		Core nodes: run task and store data
		Task node: add processing power to cluster
		
	Purchasing options
		Ondemand- reliable /pridictalble
		Reserve - min 1 yr , cost saving (Automatic pic reserved if available)
		Spot - less reliable, cheaper
	Instance configuration:
		Uniform instance groups : select single instance type and purchesing option for each node
		Instance fleet: select target capacity, mic instance types and ourchesing options (No autoscaling)
		
Running jobs on AWS?
	Ec2 instance long running , define cron jobs> doesnt scale, need to manage,simple
	cloudwatch events -> lambda function (cron schedule)
	Reactive WF- >CW events / s3 events/ api/sns /sqs/ ->>> lambda
	AWS batch -> Cronjobs, events,,, CW events >> batch 
	Use fargate , No ec2, infra, docker , farget jobs
	EMR - big data, migrate, long running cluster, big data
	
AWS Glue:
	Managed ETL-> serverless ,Glue etl jobs < S3/rds >> Redshift(warehouse)
	Glue data catalog: Catalog of datasets, crawler, all data sources possible-- RDS/dynamo/s3/jdbc compatabile db
	-> Crawler, find> write  to GLue data catalog, metadata... Run Glue ETL jobs , Athena ,Redshift spectrum , EmR
	
Redshift:
	Data warehouse is based on PostgreSQL but not used for OLTP, its OLAP
	10x better performence then other warehouses ,coloumner storage, MPP , pay as u go , not serverless
	Has a SQL interface, add quicksight and tablaw to integrate
	Data is loaded from S3 using copy command , firehose, Dynamo DB, DMS
	Based on nodes  100 + cn increase , each nde 16 tb space,  Not a multi az, all in one az, inhance networking
	Leader node- query planning and result aggrigation
	Compute node for performing the queries, computation , Managed, that means backup and restore facility 
	Launch in vpc, IAM , KMS, CW
	Redshift enhanced vpc routing, COpy and unload goes thorugh VPC
	Redshift you have to provision , use athena for query 
	
	Redshift snapshots and DR:
	Snapshots are point in time backups internally store in s3
	Snapshots are incremental
	Restore a snapshot into new cluster
	Autimated : every 8 hrs every 5gb or on a scheule , set retention
	Manual snapshots: Retained until you delete it,
	COnfigure redshift to automatically copy snapshots to another region
	SNAPSHOT_COPT_GRANT
	
	Redshift spectrum:
		Query data in s3 without loading in redshift  -- query submited to 1000s of spectrum nodes
	Redshift Workload management: Enable flexibly manage queries. Prevent short queries to get stuck in long running queries
		Define multiple query queues- Superuser queue, userdefined queue, short running, long running
		AUtomatic WLM: By redshift and manual
	Redshif concurrency scaling:
		Enables you to provide fast performance with virtually unlimited users and queries, charged /sec
		
Document DB :Aurora for mongo we can say, Mongo is used to store ,query,and index JSON data.
	Application across 3 az, auto increment, scaling
Athena and quicksight:
	SQL queries on top of your data in s3 , pay per query , op to s3
	CSV json ,parquet, ORC
	Queries are logged in cloudtrail, chained with cw logs, Great while runniing perioric queries
	
Quicksight : athena,redshift, rds, aurora.. create dashboards.

Data engineering pipeline:
S3-> Hadoop/spark /Redshift and spectrum / Athina Serverless -> Quicksight
Big data: IoT->data stream -> firehose -> s3->events / queue/ -> lambda triggers aathina >> reporting bucket -> qicksight

AWS Elastic BeanStalk;
	Wrapper for all the services we know from before, ec2 asg, eip, rds. You will have control and flexibility for deployement
	GO - JAVA - JAVA with tomcat, .net iis , nodejs, php , py , Ruby, packer builder OR use multicontainer docker / preconfigured docker
	You can write your custom platform , great to replatform from your on premises 
	Managed service, Installation and os is handelled by aws 
	Deployment stratagy is configurable but performed by beanstalk
	You have to manage application code only. 
	
	Architecture model:
		Single instance deployment , LB + asg, ASG only - non web app (Worker env)
		
	Web server vs worker env:
	More cpu /threads/ tasks / long running - > WOrker env , decoupling, use cron.yml for schedule
	
	Bluegreen deployment -- new stage , v2 , validate, R53 weighted routing, switch urls/ swapurl of bealstalk
	
AWS Opsworks:
	Chef and puppet - server configurations automatically and perform repetative action
	OPSwork is managed chef and puppet server, works great with EC2 and onprem, alternative to sso.
	Cookbooks - opswork is good , migration from other tool is not easy
	Configurations as code,  helps in consist deployement, user acc, cron , ntp , oacjages services
	Cookbooks and recipes - similarities  with ssm beanstalk cf -- works cross cloud

AWS codedeploy:
	Deploy apps, to many ec2- like v1-> v2
	Devops codedeploy agent running on ec2 
	Has integrations with ec2 asg ecs lambda 
	Ec2:
		Define appspec.yml + deployment strategy , In place updates, define hooks to verify deployment
	ASG:
		Inplace updates: -- update current exisiting ec2 instances
		Bluegreen : New asg wil be created and instances will be transferd , settings are copied , use elb 
	Lambda:
		Traffing shifting feature- lambda alias
		Pre and post traffic hooks
		Easy and automated rollbacks using cw alarms,, SAM framwork natively uses CodeDeploy
	ECS:
		Setup in ecs service defination, supports blue green deployments for amazon ecs and fargate
		A new task set is created and traffic is rerouted , check if everything is stable for X minutes old task terminated 
		
Cloudformation:
	IAC - to aws, port it across multiple account an regions
	Backbone of ecs , sevice catalog, sam --
	CF with ASG:
		Only manage asg configs, not managed unerlying ec2.
		Define success condition for the launch of your ec2 instances using creation policy,
		Define update strategy- using update policy. -- update ec2 ,create a new launch config and update the cf template.
		
	Retain data on deletes:
		You can put deletionpolicy on any resource.
		DeletePolicy=Retain
		DeletionPolicy=Snapshot
		DeletionPolicy=Delete : make sure s3 is empty before deleting and for rds db, default policy is snapshot
	Security:
		Default use permission of IAM principle
		OR assign a IAM role to stack.
		If you are creating IAM resources: provide CAPABLITY_IAM and CAPABILITY_NAMED_IAM
	Custom resources:
		Using lambda: AWS resources/services not supported by cf
				On prem resource manage by cf
				Empty one s3 bucket
				Fetch an AMI id
				CF - cross vs nested stack , use exports and function called importValues
				Nested stack - when components must be reused, how to configure alb, important to higher level stack
	Cloudformer: create cf template from resources
	Changesets: Generate and preview the cf changes before applied
	StackSetsL Deploy cf statck to multiple acc and region 
	Stack policies:Prevent accidental updates /deletes
	
Service catalog:
	New to aws, so many options to create stack, self service portal, launch only authorize products-- VM/DB/EFS
	It relies on CF: It has admins and users. Admins define products - CF template admins have to write-- > create portfolio of all templates -> Assign iam role to access portfolios
	Users: Product lists, need stack- launch product ,Will give  you provisioned product, properly used and tagged. 
	Set of cf templates user can use on basis of there iam permissions 
	
	
SAM - serverless application model
	Framework for developing and deploying serverlessapps
	Lambda apigateway dynamo sf , can help u to run lambda apigwy dynamo locally
	SAM can deploy, SAM using cf in backend
	CICD arch for sam - > Code pipeline , code commit, build, test package, +sam  --> code deploy> lambdav1/v2

AWS CDK:
	Cloud infra using your fav lang:
		Write your infra -- complied -> created cf template 
		Great for lambda /docker
		cdk cli -> generated cf template

Deployment options:
	Venilla EC2 with user data -- build ami  -- speedup deployment -- user data , auto scaling group with launch tempate , code deploy -in place updates on ec2, asg, traffic shifting, task set for ecs 
	EBS- in place all updgrades, immuteabe upgrades, bg deployment -- use opsworks chef, puppet - cannot manage asg ,, use sam for deployemnt -lambda- also leverage code deploy
	CDK  - manage code with programmin language
	
AWS Systems Manager:
	Manage your ec2 fleet and on prem systems at scale. Operational insights, detecet roblemns. Patch entire fleet. Both w and linux. Aws config + free+ cw
	Resource groups
	Insights:	Dashboard , inventory , complinace 
	Paremeter store: Store encryt=pt perameter ,
	Action: Automation , run command , session manager , patch manager , maintainence windows , state manager : define and maintain configs 
	
	SSM -> install agent on systems , on prem, Work by default for amazon linux ami 
	
	RUN COmmand : document /script / one command -- run on multiple instances, if error - stop command execution , + IAM , +CT, NO SSH needed 
	Patch manager : -- define patch baseline- predefined baselines :
		Linux:  AWS-AmazonLinux2DefaultatchBaseline, AWS-CentOSDefaultPatchBaselin , AWS-RedHatDefaultPatchBaseline ... so on
		Windows: patches are automatically approved afer 7 days, AWS-DefaultPatchBaseline: install os critical updates and secureity updates
				AWS-WindowsPredefinedPatchBaseline-OS -- same as defaultpatch baseline
				AWS-WindowsPredefinedPatchBaseline-OS-Application: Also updates microsoft applications
				
				Can define own cuustom baseline
		Steps : Define patchline -> define patchgroups (grp of instances dev/test/prod) ->maintainence window (Schedule, duration,register targets)-> Add a run commad:
				AWS-RunPatchBaseline -> Define Ratecontrol(concurrency/error/threshold) --> Monitor patch complaince using SSM Inventory
	Parameter store: secrets - secure- scalable - encryptkms -version tracking - configs, use paths, use IAM policies to path +CW events, CF template ,, Can retrive secrets from secrets manager 
	
AWS Cost allocation tags: Enable detailed reports,just like tags will show up as coloumns

AWS Cloud Migrations: THE 6R
	Rehosting : lift and shift - simple migrations , database , data, migrate as is , no cloud optimizations , could sav 30 % cost --- Server migration service -- AWS VM Impoet/export
	Replatforming : Migrate db to rds , migrate java app to beanstalk
	Repurchase: drop and shop , Moving to a different product while move to cloud , Move to SAAS , Expensive in short term but quick -- CRM ->  Selsforce
	Refactoring / Re-architecting : Rearchitect usging cloud native features , sqs, s3, lambdas. Add feature + improve performance + scale. EG: use s3 or move to serverless.
	Retire: Turn off things you dont need ,reduce amout of surface areasfor for attacks, save cost by 10-20% : Focus on maintainence
	Retain : Do nothing for now , for simplicity ,cost , importance.
	
Storage Gateway:
	Bridge between on prem data and cloud data in S3
	Usecases : disaster recovery, badkup and restore  , tired storage
	File gateway: Virtual machine bridge betwn your NFS/smb and S3, Metadata and directiory structure is preserved , S# -> NFS /smb, File gateway must have IAM role to s3
		Cache in file gateway, Can be mounted on many servers .. Server/ec2 on vpc-> FG/FG -> S3 ---> CRR/lambda/Athena/Redshift/EMR
		* Read only replicas on another data center - data fast - low latency
		* Backup and lifecycle S3-- IA and Glacier
		* S3 object versioning and restore 
		* Refresh cache api, on gateway to be notified on restore
		** S3 Object lock -- write once read many,New version created if modificaion/renaming done
	Volume gateway : Block Storage iSCSI protol  -- 32 volumes per gateway, 32 TB in cache , 16 tb in storage
												:: Cache volume -- low latency volume to most recent data from s3
												:: Stored volume -- entire dataset is on premise, scheduled backups to s3. Can create EBS snapshots from volume and restore as EBS.
	Tapes gateway : Some compainies have backup process using physical tapes, Same process in clod , VTL virtual tape liberary by S3 and glacier. Backup data using existing tape based process and iscsi.
	Works with leading backup :: YOu cant access single file with tapes , You need to restore the tape entirely. Restore first and then read.
	AWS file gateway FSX: Native access to fsx for windows file srever, Local cache for frequentl accessed data, Windows nattive SMB, NTFS, AD
	
	AWS SNOW Family: used to store and collect data at the edge, migrate data in and out :: Migration -->SNOWcone , snowball edge,  Snowmobile :: Edge computing: Sonow cone ,snowball edge
	
	
	DMS : Database migration service :: Quickly,securely migrate databses to aws, resileant and self healing.
		  Source database will remain available
		Supports homgenious migration , hetrogenious and countineous data replication using CDC , you must create ec2 for replication tasks
		Sources: Onprem, ec2 instaces databses oracle, mysql, maria,postger, mongo, sap ,db2.
		
		Azure :  azure sql db
		S3
		AWS - all including aurora
		
		Target on premm ecw, orcl,nysql, mysql server, maria, postgre sql, sap.
		Amazon rds 
		redshift, dynamodb,s3, elasticsearch,kinesis data streams, docment db
		
		AWS SCT - schema conversion tool: connvet from one engine to another
		OLTP to sql aurora
	Works over vpc peering ,vpn, direct connect , site to site, software
	Supports full load , full load, CDC 
	Oracle: It uses tde for the source using BinaryReader
			Target : Support BLOBs in tables that have a primart key and TDE
		ES: no source exist
			Target possible to migrateto dms form realtional database, DMS Cannot be used to used to replicate es data
			
		Combine snaowball and dms :: Large migrations , can be limited due to network bandwith..
			AWS SCT -- extract data -> copy to snowball --> SHip to aws ->> Load data to s3 then dms will migrate data, use CDC data will be replicated to target data store
			
AWS CART Cloud Adoption Readynes tool: 
	Helps organizations develop efficient and effective plans for cloud adoption and migrations
	Transform your idea of moving to the cloud into a detailed plan that follows aws best pratices
	Answer a set of question 
	
DR - Disaster recovery Overview
	DR types:
		On-premise - Traditional DR and very expensive
		On-premise - AWS cloud hybrid recovery 
		AWS Cloud Region A-- Cloud region B
		RPO - RTO
		
		DR strategies--
			Backup and restore  -- High RPO -- cost of only storing , high rto. snapshot, s3, lifecycle 
			Pilot light -- Small version of the app is always running in the cloud -- useful for the critical core , very similar to backup and restore -- lower rpo rto 
			Warm standby -- full system is up and running but at minimum size , on disaster scale it
			Hot site - multi site appoach -- full production scale -- high cost -- less rpo rto
			All cloud -- aurora master slave multi region
AWS FIS - falt injection simukator
	 Chaos enginering, sdden cpu oir memor spikes
	 
VM migration service :
	Application discovery services :
		Plan migration projets by gathering information about on-primises data center -- map dependencies, gather info about servers
		Agenteless dicovery - Application discovery agentless connecter this is OVA package can be deployed on vmware host
		vm inventory , configs , performance histiry such as cpu disk and memory, OS Aghnostic
		Agent baes discoveru :: system configs , performance , processes , and network details betn system. map data with all other servers and there agents.Like some server talk to one another 
		View data in migration hub or export csv	 
		
	Application Migration service (SMS or CLOUD ENDURE) : The evolution of cloudendure migration , replacing aws server migration service
		Lift and shift - rehost solution which simplidy migrating application to aws, Converts your physical, virtual and cloud based servers to run natively on aws 
		
	AWS Elastic Disaster recovery:
		Cloudendure dr service - Quickly recover your physical, virtua and cloud based servers into aws
		Protect from ransomware and most critical databases  -- contineous block level replication 
		Failover into minutes
		
VPC:
		CIDR block of IP address
		IP range- defined /26 is range of 64 ip -- Used everywhere , routetable , vpc, subnet etc eyc
		Private ip: 10 .0.0.0 -- 10.255.255.255 (10.0.0.0/8) -- big networks
		172.16.0.0/12  -- default aws one
		192.168.0.0/16 -- home networks
		
		Else is public ip
		
		List of cidr block and much not be changed min size is /28 and max is /16 65536 ip
		VPC is private and private cird range is allowed in vpc -- subnet is a subset of vpc cidr , all instances in subnet are private,,
		The first 4 ip and last ip is preserved by aws for networking purposes
		Route table:
			Used to control where the netrowk trafic is redireccated to , can be assosiasted with specific subnets . Like one subnet to another  
			More specific routing rule is always followed 
			
		IGW : COnnect vpc to internet, HA and scales horizontally, ACt a a NAT for instnaces that have public ipv4/ipv6
		Public subnets have routes 0.0.0.0/0 to igw , instances must have public ip to speack to internet 
		Private subnet access internet through a NAT instance with nat gateway, edit that route 0000 routes to nat 
		
		NAT instane: Ec2 instance that you deploy in public subnet , updtate the route in table , not resileant to failure, cheaper, manage failover yourself
		Nat gateway: sacles automatic, managed by aws , single az failure . Setup MUltiple nat gateway for HA, Has a elastic Ip external service see the ip of the nat gateway as the source 
		NACL : Stateless firewall defined atthe subnet level, applies to all instances within  -- Allow and deny rules
		Stateless -- any return traffice must be allowed by rules
		Quickly and cheaply block specific traffic ip address
		SGW: Instance level , allow rules, stateful. Can refrencet sg of the same region 
		
		VPC flow logs:  :Log internet traffing flowing through vpc , can be defined at  VPC level , subnet levek or eni level. Helpful in denied internet traffic, can be sent to cw logs and s3 
		Bastion Hosts: public ec2 instance through a public ec2 instance ssh, no managed bastion host by aws, need to manage by urself 
		SSM sessions manager is a more secure way to remote contron SSH.
		IPV6- are public 
		
VPC - Peering :
	Connect two vp , privately using AWS network, make them behave as if they were in the same network -- non overlapping cidr -- update route table.
	Peering is not transitive ..
	You can do vpc peering in your own account or another aws account-- Must update route tables in each vpc subnets to ensure instanes communicate
	You can refrence a sg of peered vpc and that works cross account 
	VPC peering can work interregion and cross account
	Longest prefix match: Most specific route  /32 
	
	Invalid configurations:
		2 vpc same side cannot connect  -- also true for ipv6 , no transative vpc peering , no edge to edge routing
		
VPC endpoint :
	allow aws service to use private netrowk insted of internet.. Scale horizontally and they are redundent
	No more igw nat etc
	Vpc endpoint gateway -- only for dynamo db, 1 gateway per vpc , update route table entries to make it work , gateway is on vpc level, dns resoulton must e enabled on vpc ,can use hostname for s3 insted of ip , cannot extend out of vpc-- vpn ,dx tgw
	Vpc endpoint interface for all , ENI -- has private hostname , with eni we have sgs , Private dns setting need to be enabled with endbpoint.
				Public hostname of a service will resolve to private endpoint
				Enable dns hostname , enable dns support must be set to true , interfaces are shareable 

VPC endpoint policies :
		JSON document to control access to a service -- like if some user want to access some specific sqs queue with endpoint , does not ovveride or replace iam user policies
		
AWS PrivateLink:
	VPC endpoint services:
		Most secure and scalable way to expose a service tp 1000v of VPC either own or other accounts
		Does not require vpc peering , igw or nat , or route tables.
		Create NLB in service VPC and ENI in customer vpc --- private link will create a private connection betwn them .
		NLB is in multi az then eni must be in multi az , fault tolerant 
		You can do web filtering 
		
VPN:
	SITE TO SITE -- AWS managed vpn
			Data center + VPC
			Onprem : Setup software or hardware vpn appliance, on prem vpn should be accicible over a public ip 
			AWS: Setup VGW -Virtual private gateway,, setup a customer gateway 
			update routetable and router -- static or dynamic BGP border gateway protocol, dont need to update routetable ,need to specify asn of both 
			
			Two vpn connection will be created for redundenency, encrypted using ipsec 
			Use aws global accelarator to accrt world wide network
	Clodud hub: uptp 10 cgw to vgw
			Low cost hub and spoke model , secure ,vpn ,goes over public internet , failover may happen 
			
AWS client VPN :
	Cpnnect from your computer - open vpn to your private network 
	
Software VPN :: Site to site and also you can choose your own software vpn, public subnet ec2
VPN to multiple vpc: VPC -> create saperate vpn connection for each vpc  -- USE direct connect also 
			Create a shared services vpc - create vpn connetion betn shared services vpc and on prem
			Then, replicate service or cerate a fleet of proxies -- now we can do vpc peering with each vpc 
			
Direct connect : 
	Gives you a dedicated private connection from a remote network to vpc , Dedicated connection must be setup bwtn DC and AWS DC locations,
	More expensive then your VPN soln, BY pass ISP , reduce network cost, increase bandwith, not redundent by default must setup a failover / vpn 
