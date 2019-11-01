# replication-sharding

### Initial state:
<pre><code>
rs0:PRIMARY> rs.status()
{
	"set" : "rs0",
	"date" : ISODate("2019-11-02T13:43:39.309Z"),
	"myState" : 1,
	"term" : NumberLong(1),
	"syncingTo" : "",
	"syncSourceHost" : "",
	"syncSourceId" : -1,
	"heartbeatIntervalMillis" : NumberLong(2000),
	"majorityVoteCount" : 2,
	"writeMajorityCount" : 2,
	"optimes" : {
		"lastCommittedOpTime" : {
			"ts" : Timestamp(1572702217, 1),
			"t" : NumberLong(1)
		},
		"lastCommittedWallTime" : ISODate("2019-11-02T13:43:37.870Z"),
		"readConcernMajorityOpTime" : {
			"ts" : Timestamp(1572702217, 1),
			"t" : NumberLong(1)
		},
		"readConcernMajorityWallTime" : ISODate("2019-11-02T13:43:37.870Z"),
		"appliedOpTime" : {
			"ts" : Timestamp(1572702217, 1),
			"t" : NumberLong(1)
		},
		"durableOpTime" : {
			"ts" : Timestamp(1572702217, 1),
			"t" : NumberLong(1)
		},
		"lastAppliedWallTime" : ISODate("2019-11-02T13:43:37.870Z"),
		"lastDurableWallTime" : ISODate("2019-11-02T13:43:37.870Z")
	},
	"lastStableRecoveryTimestamp" : Timestamp(1572702187, 1),
	"lastStableCheckpointTimestamp" : Timestamp(1572702187, 1),
	"electionCandidateMetrics" : {
		"lastElectionReason" : "electionTimeout",
		"lastElectionDate" : ISODate("2019-11-02T12:42:06.854Z"),
		"termAtElection" : NumberLong(1),
		"lastCommittedOpTimeAtElection" : {
			"ts" : Timestamp(0, 0),
			"t" : NumberLong(-1)
		},
		"lastSeenOpTimeAtElection" : {
			"ts" : Timestamp(1572698515, 1),
			"t" : NumberLong(-1)
		},
		"numVotesNeeded" : 2,
		"priorityAtElection" : 1,
		"electionTimeoutMillis" : NumberLong(10000),
		"numCatchUpOps" : NumberLong(27017),
		"newTermStartDate" : ISODate("2019-11-02T12:42:07.766Z"),
		"wMajorityWriteAvailabilityDate" : ISODate("2019-11-02T12:42:08.801Z")
	},
	"members" : [
		{
			"_id" : 0,
			"name" : "instance1:27017",
			"ip" : "172.31.28.133",
			"health" : 1,
			"state" : 2,
			"stateStr" : "SECONDARY",
			"uptime" : 3702,
			"optime" : {
				"ts" : Timestamp(1572702217, 1),
				"t" : NumberLong(1)
			},
			"optimeDurable" : {
				"ts" : Timestamp(1572702217, 1),
				"t" : NumberLong(1)
			},
			"optimeDate" : ISODate("2019-11-02T13:43:37Z"),
			"optimeDurableDate" : ISODate("2019-11-02T13:43:37Z"),
			"lastHeartbeat" : ISODate("2019-11-02T13:43:39.228Z"),
			"lastHeartbeatRecv" : ISODate("2019-11-02T13:43:39.228Z"),
			"pingMs" : NumberLong(0),
			"lastHeartbeatMessage" : "",
			"syncingTo" : "instance2:27017",
			"syncSourceHost" : "instance2:27017",
			"syncSourceId" : 1,
			"infoMessage" : "",
			"configVersion" : 1
		},
		{
			"_id" : 1,
			"name" : "instance2:27017",
			"ip" : "172.31.21.5",
			"health" : 1,
			"state" : 1,
			"stateStr" : "PRIMARY",
			"uptime" : 3819,
			"optime" : {
				"ts" : Timestamp(1572702217, 1),
				"t" : NumberLong(1)
			},
			"optimeDate" : ISODate("2019-11-02T13:43:37Z"),
			"syncingTo" : "",
			"syncSourceHost" : "",
			"syncSourceId" : -1,
			"infoMessage" : "",
			"electionTime" : Timestamp(1572698526, 1),
			"electionDate" : ISODate("2019-11-02T12:42:06Z"),
			"configVersion" : 1,
			"self" : true,
			"lastHeartbeatMessage" : ""
		},
		{
			"_id" : 2,
			"name" : "instance3:27017",
			"ip" : "172.31.20.69",
			"health" : 1,
			"state" : 2,
			"stateStr" : "SECONDARY",
			"uptime" : 3702,
			"optime" : {
				"ts" : Timestamp(1572702217, 1),
				"t" : NumberLong(1)
			},
			"optimeDurable" : {
				"ts" : Timestamp(1572702217, 1),
				"t" : NumberLong(1)
			},
			"optimeDate" : ISODate("2019-11-02T13:43:37Z"),
			"optimeDurableDate" : ISODate("2019-11-02T13:43:37Z"),
			"lastHeartbeat" : ISODate("2019-11-02T13:43:39.228Z"),
			"lastHeartbeatRecv" : ISODate("2019-11-02T13:43:39.229Z"),
			"pingMs" : NumberLong(0),
			"lastHeartbeatMessage" : "",
			"syncingTo" : "instance2:27017",
			"syncSourceHost" : "instance2:27017",
			"syncSourceId" : 1,
			"infoMessage" : "",
			"configVersion" : 1
		}
	],
	"ok" : 1,
	"$clusterTime" : {
		"clusterTime" : Timestamp(1572702217, 1),
		"signature" : {
			"hash" : BinData(0,"AAAAAAAAAAAAAAAAAAAAAAAAAAA="),
			"keyId" : NumberLong(0)
		}
	},
	"operationTime" : Timestamp(1572702217, 1)
}
</code></pre>
<pre><code>
rs0:PRIMARY> rs.config()
{
	"_id" : "rs0",
	"version" : 1,
	"protocolVersion" : NumberLong(1),
	"writeConcernMajorityJournalDefault" : true,
	"members" : [
		{
			"_id" : 0,
			"host" : "instance1:27017",
			"arbiterOnly" : false,
			"buildIndexes" : true,
			"hidden" : false,
			"priority" : 1,
			"tags" : {
				
			},
			"slaveDelay" : NumberLong(0),
			"votes" : 1
		},
		{
			"_id" : 1,
			"host" : "instance2:27017",
			"arbiterOnly" : false,
			"buildIndexes" : true,
			"hidden" : false,
			"priority" : 1,
			"tags" : {
				
			},
			"slaveDelay" : NumberLong(0),
			"votes" : 1
		},
		{
			"_id" : 2,
			"host" : "instance3:27017",
			"arbiterOnly" : false,
			"buildIndexes" : true,
			"hidden" : false,
			"priority" : 1,
			"tags" : {
				
			},
			"slaveDelay" : NumberLong(0),
			"votes" : 1
		}
	],
	"settings" : {
		"chainingAllowed" : true,
		"heartbeatIntervalMillis" : 2000,
		"heartbeatTimeoutSecs" : 10,
		"electionTimeoutMillis" : 10000,
		"catchUpTimeoutMillis" : -1,
		"catchUpTakeoverDelayMillis" : 30000,
		"getLastErrorModes" : {
			
		},
		"getLastErrorDefaults" : {
			"w" : 1,
			"wtimeout" : 0
		},
		"replicaSetId" : ObjectId("5dbd7993231fa406278ecc3e")
	}
}
</code></pre>