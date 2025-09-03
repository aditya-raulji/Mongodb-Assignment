

## Section A. CRUD Basics (Answers)

**Q1. Insert a new company "Tesla"**

```javascript
db.companies.insertOne({
  name: "Tesla",
  location: "Bangalore",
  salaryBand: { base: 29, bonus: 4, stock: 6 },
  hiringCriteria: { cgpa: 7.0, skills: ["DSA", "Python", "Distributed Systems"], experience: "1-2 years" },
  interviewRounds: [
    { round: 1, type: "OA" },
    { round: 2, type: "Technical" },
    { round: 3, type: "HR" }
  ],
  benefits: ["Relocation", "WFH"],
  headcount: 800
})
```


---

**Q2. Insert multiple companies ("Stripe", "Coinbase")**

```javascript
db.companies.insertMany([
  { name: "Stripe", location: "Bangalore", salaryBand: { base: 40, bonus: 8, stock: 12 } },
  { name: "Coinbase", location: "Hyderabad", salaryBand: { base: 38, bonus: 6, stock: 15 } }
])
```



---

**Q3. Find all companies**

```javascript
db.companies.find()
```


---

**Q4. Find one company in Bangalore**

```javascript
db.companies.findOne({ location: "Bangalore" })
```


---

**Q5. Companies with base > 30 LPA**

```javascript
db.companies.find({ "salaryBand.base": { $gt: 30 } })
```


---

**Q6. Companies in Hyderabad**

```javascript
db.companies.find({ location: "Hyderabad" })
```


---

**Q7. CGPA requirement >= 8.0**

```javascript
db.companies.find({ "hiringCriteria.cgpa": { $gte: 8.0 } })
```


---

**Q8. Companies requiring "System Design"**

```javascript
db.companies.find({ "hiringCriteria.skills": "System Design" })
```


---

**Q9. Companies offering "Relocation"**

```javascript
db.companies.find({ benefits: "Relocation" })
```


---

**Q10. Companies with stock >= 15**

```javascript
db.companies.find({ "salaryBand.stock": { $gte: 15 } })
```


---

**Q11. At least 4 interview rounds**

```javascript
db.companies.find({ "interviewRounds.3": { $exists: true } })
```


---

**Q12. Headcount > 5000**

```javascript
db.companies.find({ headcount: { $gt: 5000 } })
```


---

**Q13. Insert company with only `name`, `location`**

```javascript
db.companies.insertOne({ name: "Freshworks", location: "Chennai" })
```


---

**Q14. Update Amazon’s bonus to 6**

```javascript
db.companies.updateOne(
  { name: "Amazon" },
  { $set: { "salaryBand.bonus": 6 } }
)
```


---

**Q15. Add "Free Snacks" to all Hyderabad companies**

```javascript
db.companies.updateMany(
  { location: "Hyderabad" },
  { $addToSet: { benefits: "Free Snacks" } }
)
```


---

**Q16. Add skill "Python" to Google**

```javascript
db.companies.updateOne(
  { name: "Google" },
  { $addToSet: { "hiringCriteria.skills": "Python" } }
)
```

---

**Q17. Remove "Gym" from Microsoft**

```javascript
db.companies.updateOne(
  { name: "Microsoft" },
  { $pull: { benefits: "Gym" } }
)
```

---

**Q18. Replace salaryBand for Netflix**

```javascript
db.companies.updateOne(
  { name: "Netflix" },
  { $set: { salaryBand: { base: 40, bonus: 8, stock: 20 } } }
)
```

---

**Q19. Delete Infosys**

```javascript
db.companies.deleteOne({ name: "Infosys" })
```

---

**Q20. Delete all companies base < 10**

```javascript
db.companies.deleteMany({ "salaryBand.base": { $lt: 10 } })
```


---

**Q21. Add field isTopTier to Google**

```javascript
db.companies.updateOne(
  { name: "Google" },
  { $set: { isTopTier: true } }
)
```

---

**Q22. Increase Amazon’s stock by 2**

```javascript
db.companies.updateOne(
  { name: "Amazon" },
  { $inc: { "salaryBand.stock": 2 } }
)
```

---

**Q23. Rename headcount → employeeCount**

```javascript
db.companies.updateMany({}, { $rename: { headcount: "employeeCount" } })
```

---

**Q24. Remove bonus from salaryBand**

```javascript
db.companies.updateMany({}, { $unset: { "salaryBand.bonus": "" } })
```

---

**Q25. Insert 5 dummy companies**

```javascript
db.companies.insertMany([
  { name: "Dummy1" },
  { name: "Dummy2" },
  { name: "Dummy3" },
  { name: "Dummy4" },
  { name: "Dummy5" }
])
```

---

**Q26. Delete all dummy companies**

```javascript
db.companies.deleteMany({ name: { $regex: /^Dummy/ } })
```

---

**Q27. Project only name & salaryBand**

```javascript
db.companies.find({}, { name: 1, salaryBand: 1 })
```

---

**Q28. Exclude `_id`**

```javascript
db.companies.find({}, { _id: 0, name: 1, location: 1 })
```

---

**Q29. Microsoft name + benefits only**

```javascript
db.companies.find({ name: "Microsoft" }, { name: 1, benefits: 1 })
```

---

**Q30. Count Bangalore companies**

```javascript
db.companies.countDocuments({ location: "Bangalore" })
```


---

**Q31. Count CGPA >= 7.0**

```javascript
db.companies.countDocuments({ "hiringCriteria.cgpa": { $gte: 7.0 } })
```

---

**Q32. Distinct locations**

```javascript
db.companies.distinct("location")
```


---

**Q33. Distinct benefits**

```javascript
db.companies.distinct("benefits")
```


---

**Q34. Any company stock = 20**

```javascript
db.companies.findOne({ "salaryBand.stock": 20 })
```


---

**Q35. Insert nested perks**

```javascript
db.companies.updateOne(
  { name: "Swiggy" },
  { $set: { perks: { transport: true } } }
)
```

---

**Q36. Push new round in Meta**

```javascript
db.companies.updateOne(
  { name: "Meta" },
  { $push: { interviewRounds: { round: 5, type: "CTO Interview" } } }
)
```

---

**Q37. Remove "HR" round from Amazon**

```javascript
db.companies.updateOne(
  { name: "Amazon" },
  { $pull: { interviewRounds: { type: "HR" } } }
)
```

---

**Q38. Add "Health Insurance" if not exists in Swiggy**

```javascript
db.companies.updateOne(
  { name: "Swiggy" },
  { $addToSet: { benefits: "Health Insurance" } }
)
```

---

**Q39. Increase base salary by 2 for Bangalore companies**

```javascript
db.companies.updateMany(
  { location: "Bangalore" },
  { $inc: { "salaryBand.base": 2 } }
)
```

---

**Q40. Delete Delhi companies**

```javascript
db.companies.deleteMany({ location: "Delhi" })
```


---

## Section B. Advanced Queries


**Q41. Companies with base between 25–35**

```javascript
db.companies.find({ "salaryBand.base": { $gte: 25, $lte: 35 } })
```


---

**Q42. Companies with stock < 10**

```javascript
db.companies.find({ "salaryBand.stock": { $lt: 10 } })
```


---

**Q43. Bonus > 5 AND stock > 10**

```javascript
db.companies.find({ "salaryBand.bonus": { $gt: 5 }, "salaryBand.stock": { $gt: 10 } })
```


---

**Q44. Base >= 30 OR stock >= 12**

```javascript
db.companies.find({
  $or: [
    { "salaryBand.base": { $gte: 30 } },
    { "salaryBand.stock": { $gte: 12 } }
  ]
})
```


---

**Q45. Companies NOT requiring "OS"**

```javascript
db.companies.find({ "hiringCriteria.skills": { $ne: "OS" } })
```


---

**Q46. At least one skill from \["Java", "C++"]**

```javascript
db.companies.find({ "hiringCriteria.skills": { $in: ["Java", "C++"] } })
```


---

**Q47. Must require BOTH "DSA" and "System Design"**

```javascript
db.companies.find({ "hiringCriteria.skills": { $all: ["DSA", "System Design"] } })
```


---

**Q48. Companies not offering WFH**

```javascript
db.companies.find({ benefits: { $ne: "WFH" } })
```


---

**Q49. Companies with >3 benefits**

```javascript
db.companies.find({ benefits: { $exists: true, $size: { $gt: 3 } } })
```


```javascript
db.companies.aggregate([
  { $project: { name: 1, benefitCount: { $size: "$benefits" } } },
  { $match: { benefitCount: { $gt: 3 } } }
])
```


---

**Q50. Exactly 4 interview rounds**

```javascript
db.companies.find({ "interviewRounds.3": { $exists: true }, "interviewRounds.4": { $exists: false } })
```


---

**Q51. Employee count > 2000**

```javascript
db.companies.find({ employeeCount: { $gt: 2000 } })
```


---

**Q52. Salaries in multiples of 5**

```javascript
db.companies.find({ "salaryBand.base": { $mod: [5, 0] } })
```


---

**Q53. CGPA in \[6.5, 7.0, 7.5]**

```javascript
db.companies.find({ "hiringCriteria.cgpa": { $in: [6.5, 7.0, 7.5] } })
```


---

**Q54. Companies NOT in Bangalore**

```javascript
db.companies.find({ location: { $ne: "Bangalore" } })
```


---

**Q55. Skills ending with "Design"**

```javascript
db.companies.find({ "hiringCriteria.skills": { $regex: /Design$/ } })
```


---

**Q56. Companies starting with "A"**

```javascript
db.companies.find({ name: { $regex: /^A/ } })
```


---

**Q57. Case-insensitive search "amazon"**

```javascript
db.companies.find({ name: { $regex: /^amazon$/i } })
```


---

**Q58. Where stock field exists**

```javascript
db.companies.find({ "salaryBand.stock": { $exists: true } })
```


---

**Q59. Where perks field does NOT exist**

```javascript
db.companies.find({ perks: { $exists: false } })
```


---

**Q60. Salary base must be a number**

```javascript
db.companies.find({ "salaryBand.base": { $type: "number" } })
```


---

**Q61. Sort base ascending**

```javascript
db.companies.find().sort({ "salaryBand.base": 1 })
```


---

**Q62. Sort base descending**

```javascript
db.companies.find().sort({ "salaryBand.base": -1 })
```


---

**Q63. Sort by bonus then stock**

```javascript
db.companies.find().sort({ "salaryBand.bonus": 1, "salaryBand.stock": 1 })
```

---

**Q64. Limit to top 5 highest base**

```javascript
db.companies.find().sort({ "salaryBand.base": -1 }).limit(5)
```


---

**Q65. Skip first 5 and return next 5**

```javascript
db.companies.find().sort({ "salaryBand.base": -1 }).skip(5).limit(5)
```

---

**Q66. Company with maximum base**

```javascript
db.companies.find().sort({ "salaryBand.base": -1 }).limit(1)
```


---

**Q67. Company with minimum CGPA**

```javascript
db.companies.find().sort({ "hiringCriteria.cgpa": 1 }).limit(1)
```


---

**Q68. First 3 alphabetically**

```javascript
db.companies.find().sort({ name: 1 }).limit(3)
```


---

**Q69. Companies with "Technical" round**

```javascript
db.companies.find({ "interviewRounds.type": "Technical" })
```


---

**Q70. Round 2 = "System Design"**

```javascript
db.companies.find({ "interviewRounds.1.type": "System Design" })
```


---

**Q71. InterviewRounds length > 3**

```javascript
db.companies.find({ "interviewRounds.3": { $exists: true } })
```


---

**Q72. Second benefit = "WFH"**

```javascript
db.companies.find({ "benefits.1": "WFH" })
```


---

**Q73. Must have \["DSA", "Java"]**

```javascript
db.companies.find({ "hiringCriteria.skills": { $all: ["DSA", "Java"] } })
```


---

**Q74. SalaryBand elemMatch (base > 25 and stock > 5)**

```javascript
db.companies.find({ salaryBand: { $elemMatch: { base: { $gt: 25 }, stock: { $gt: 5 } } } })
```


```javascript
db.companies.find({ "salaryBand.base": { $gt: 25 }, "salaryBand.stock": { $gt: 5 } })
```

---

**Q75. Location in \[Hyderabad, Bangalore]**

```javascript
db.companies.find({ location: { $in: ["Hyderabad", "Bangalore"] } })
```

---

**Q76. Location not in \[Mumbai, Pune]**

```javascript
db.companies.find({ location: { $nin: ["Mumbai", "Pune"] } })
```

---

**Q77. Base closest to 30**

```javascript
db.companies.aggregate([
  { $project: { name: 1, base: "$salaryBand.base", diff: { $abs: { $subtract: ["$salaryBand.base", 30] } } } },
  { $sort: { diff: 1 } },
  { $limit: 1 }
])
```


---

**Q78. Exclude salaries < 20**

```javascript
db.companies.find({ "salaryBand.base": { $not: { $lt: 20 } } })
```

---

**Q79. Bonus < base/10**

```javascript
db.companies.find({ $expr: { $lt: ["$salaryBand.bonus", { $divide: ["$salaryBand.base", 10] }] } })
```

---

**Q80. Exactly 2 benefits**

```javascript
db.companies.find({ benefits: { $size: 2 } })
```


---

**Q81. Project totalComp**

```javascript
db.companies.aggregate([
  { $project: { name: 1, totalComp: { $add: ["$salaryBand.base", "$salaryBand.bonus", "$salaryBand.stock"] } } }
])
```

---

**Q82. totalComp > 45**

```javascript
db.companies.aggregate([
  { $project: { name: 1, totalComp: { $add: ["$salaryBand.base", "$salaryBand.bonus", "$salaryBand.stock"] } } },
  { $match: { totalComp: { $gt: 45 } } }
])
```


---

**Q83. Sort by totalComp**

```javascript
db.companies.aggregate([
  { $project: { name: 1, totalComp: { $add: ["$salaryBand.base", "$salaryBand.bonus", "$salaryBand.stock"] } } },
  { $sort: { totalComp: -1 } }
])
```

---

**Q84. Multiply stock by 2**

```javascript
db.companies.updateMany({}, { $mul: { "salaryBand.stock": 2 } })
```

---

**Q85. Ensure bonus >= 5**

```javascript
db.companies.updateMany({}, { $max: { "salaryBand.bonus": 5 } })
```

---

**Q86. Cap base at 35**

```javascript
db.companies.updateMany({}, { $min: { "salaryBand.base": 35 } })
```

---

**Q87. Ensure unique WFH**

```javascript
db.companies.updateMany({}, { $addToSet: { benefits: "WFH" } })
```

---

**Q88. Array filter → change 3rd round**

```javascript
db.companies.updateMany(
  {},
  { $set: { "interviewRounds.$[elem].type": "Tech Screen" } },
  { arrayFilters: [{ "elem.round": 3 }] }
)
```

---

**Q89. Add currentDate**

```javascript
db.companies.updateMany({}, { $currentDate: { lastUpdated: true } })
```

---

**Q90. Delete companies without benefits**

```javascript
db.companies.deleteMany({ benefits: { $exists: false } })
```

---

**Q91. Upsert Tesla**

```javascript
db.companies.updateOne(
  { name: "Tesla" },
  { $set: { location: "Bangalore" } },
  { upsert: true }
)
```

---

**Q92. Exclude salaryBand**

```javascript
db.companies.find({}, { salaryBand: 0 })
```

---

**Q93. Project doubleStock**

```javascript
db.companies.aggregate([
  { $project: { name: 1, doubleStock: { $multiply: ["$salaryBand.stock", 2] } } }
])
```

---

**Q94. Name length = 6**

```javascript
db.companies.find({ $expr: { $eq: [{ $strLenCP: "$name" }, 6] } })
```


---

**Q95. base % 2 = 0**

```javascript
db.companies.find({ "salaryBand.base": { $mod: [2, 0] } })
```

---

**Q96. headcount > 2000 (\$where)**

```javascript
db.companies.find({ $where: "this.employeeCount > 2000" })
```

---

**Q97. Text search "Java"**
(First, index on skills)

```javascript
db.companies.createIndex({ "hiringCriteria.skills": "text" })
db.companies.find({ $text: { $search: "Java" } })
```

---

**Q98. Case-insensitive sort**

```javascript
db.companies.find().collation({ locale: "en", strength: 2 }).sort({ name: 1 })
```

---

**Q99. Benefits type = array**

```javascript
db.companies.find({ benefits: { $type: "array" } })
```

---

**Q100. Benefits include "Free Meals"**

```javascript
db.companies.find({ benefits: "Free Meals" })
```


---
