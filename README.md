# mongoDB-assignment01

use todoApp
switched to db todoApp
db.createCollection("task")
{ ok: 1 }

db.tasks.insertMany([
  {
    task: "Buy maggie", 
    status: "pending",
    createdAt: new Date(),
    updatedAt: new Date()
  },
  { 
    task: "Complete assignment", 
    status: "pending",
    createdAt: new Date(),
    updatedAt: new Date()
  },
  { 
    task: "Call family", 
    status: "completed",
    createdAt: new Date(),
    updatedAt: new Date()
  }
)

{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('6837367e09b1f0438f0b5c47'),
    '1': ObjectId('6837367e09b1f0438f0b5c48'),
    '2': ObjectId('6837367e09b1f0438f0b5c49')
  }
}

db.tasks.find().pretty()

{
  _id: ObjectId('6837367e09b1f0438f0b5c47'),
  task: 'Buy maggie',
  status: 'pending',
  createdAt: 2025-05-28T16:14:54.817Z,
  updatedAt: 2025-05-28T16:14:54.817Z
}

{
  _id: ObjectId('6837367e09b1f0438f0b5c48'),
  task: 'Complete assignment',
  status: 'pending',
  createdAt: 2025-05-28T16:14:54.817Z,
  updatedAt: 2025-05-28T16:14:54.817Z
}

{
  _id: ObjectId('6837367e09b1f0438f0b5c49'),
  task: 'Call family',
  status: 'completed',
  createdAt: 2025-05-28T16:14:54.817Z,
  updatedAt: 2025-05-28T16:14:54.817Z
}
db.tasks.countDocuments()
3
db.tasks.updateOne(
  { task: "Buy maggie" },
  { 
    $set: { 
      status: "completed",
      updatedAt: new Date()
    }
  }
)

{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}

db.tasks.deleteOne({ task: "Call family" })

{
  acknowledged: true,
  deletedCount: 1
}

db.tasks.insertOne({
  task: "Pay electricity bill",
  status: "pending",
  dueDate: new Date("2025-06-05"),
  priority: "high",
  createdAt: new Date(),
  updatedAt: new Date()
})

{
  acknowledged: true,
  insertedId: ObjectId('683736d209b1f0438f0b5c4a')
}

db.tasks.find({ status: "pending" }).pretty()

{
  _id: ObjectId('6837367e09b1f0438f0b5c48'),
  task: 'Complete assignment',
  status: 'pending',
  createdAt: 2025-05-28T16:14:54.817Z,
  updatedAt: 2025-05-28T16:14:54.817Z
}

{
  _id: ObjectId('683736d209b1f0438f0b5c4a'),
  task: 'Pay electricity bill',
  status: 'pending',
  dueDate: 2025-06-05T00:00:00.000Z,
  priority: 'high',
  createdAt: 2025-05-28T16:16:18.836Z,
  updatedAt: 2025-05-28T16:16:18.836Z
}

db.tasks.find({ 
  dueDate: { $lt: new Date("2025-06-10") }
}).pretty()
{
  _id: ObjectId('683736d209b1f0438f0b5c4a'),
  task: 'Pay electricity bill',
  status: 'pending',
  dueDate: 2025-06-05T00:00:00.000Z,
  priority: 'high',
  createdAt: 2025-05-28T16:16:18.836Z,
  updatedAt: 2025-05-28T16:16:18.836Z
}

// Tasks updated in last 24 hours

db.tasks.find({
  updatedAt: { $gt: new Date(Date.now() - 24*60*60*1000) }
}).pretty()
{
  _id: ObjectId('6837367e09b1f0438f0b5c47'),
  task: 'Buy maggie',
  status: 'completed',
  createdAt: 2025-05-28T16:14:54.817Z,
  updatedAt: 2025-05-28T16:15:47.012Z
}
{
  _id: ObjectId('6837367e09b1f0438f0b5c48'),
  task: 'Complete assignment',
  status: 'pending',
  createdAt: 2025-05-28T16:14:54.817Z,
  updatedAt: 2025-05-28T16:14:54.817Z
}
{
  _id: ObjectId('683736d209b1f0438f0b5c4a'),
  task: 'Pay electricity bill',
  status: 'pending',
  dueDate: 2025-06-05T00:00:00.000Z,
  priority: 'high',
  createdAt: 2025-05-28T16:16:18.836Z,
  updatedAt: 2025-05-28T16:16:18.836Z
}
