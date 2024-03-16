## APIs documentation
- PROXY `https://api.apexunifier.tech/`, add proxy in `package.json`
```
{
    "proxy": "https://api.apexunifier.tech/"
}
```
### User apis

- POST `/api/user/login`, login user

require email, password.

responce `json({ email: user.email, token, accountType: "user", Id: Id });` or `json({ error: error.message })`

- POST `/api/user/signup`, signup user

require name, phoneNo, email, password.

responce  
 `json({email: newUser.email,token,accountType: "user", Id: newUser._id,})`
or `json({ error: error.message })`

## Vacancy apis

### Vacancy Model

```js
    title: {
      type: String,
      required: [true, "Title is required"],
    },
    description: {
      type: String,
      required: [true, "Description is required"],
    },
    requirements: {
      type: [String],
      required: [true, "Requirements are required"],
    },
    responsibilities: {
      type: [String],
      required: [true, "Responsibilities are required"],
    },
    location: {
      type: String,
      required: [true, "Location is required"],
    },
    expectedSalary: {
      minSalary: {
        type: Number,
        required: [true, "Minimum salary is required"],
      },
      maxSalary: {
        type: Number,
        required: [true, "Maximum salary is required"],
      },
    },
    benefits: {
      type: [String],
    },
    skillsRequired: {
      type: [String],
      required: [true, "Skills required are required"],
    },
    // Reference to the CompanySchema using company id
    company: {
      type: Schema.Types.ObjectId,
      ref: "Company",
      required: [true, "Company is required"],
    },
    status: {
      type: String,
      enum: ["open", "closed"],
      default: "open",
    },
    numberOfVacanciesAvailable: {
      type: Number,
      required: [true, "Number of vacancies available is required"],
    }
```

- GET `/api/vacancy/` getAllVacancies,

responce `json({ success: true, vacancies: vacancies })` or `json({success: false,message: "Failed to fetch vacancies",error: error.message,})`

- POST `/api/vacancy/create` createVacancy

require // see vacancy model all feilds require

responce `json({
      success: true,
      message: "Vacancy created successfully",
      vacancy: newVacancy, 
    })`
or
`json({
      success: false,
      message: "Failed to create vacancy",
      error: error.message,
    })`

- GET `/api/vacancy/:id` getVacancyById

responce -

```
json({
      success: true,
      vacancy: vacancy,
    })
```

or

```
json({
        success: false,
        message: "Vacancy not found",
      })
```

or

```
json({
      success: false,
      message: "Failed to fetch vacancy",
      error: error.message,
    })
```

- DELETE `/api/vacancy/:id` deleteVacancy

responce -

```
json({
      success: true,
      message: "Vacancy deleted successfully",
      vacancy: deletedVacancy,
    })
```

or

```
json({
        success: false,
        message: "Vacancy not found",
      })
```

or

```
json({
      success: false,
      message: "Failed to delete vacancy",
      error: error.message,
    })
```

- GET `/api/vacancy/company/:companyId` getAllVacanciesForCompany,

responce
`json({ success: true, vacancies: vacancies })`
or

```
json({
      success: false,
      message: "Failed to fetch vacancies for the company",
      error: error.message,
    })
```

## Company Apis

- POST `/api/company/login` login company

request email, password

responce
`json({ email, token, Id: Id, accountType: "company" })`
or
`json({ error: error.message })`

- POST `/api/company/signup` signup company

request companyName, email, password, yearOfEstablishment, fieldsOfWork

responce
`json({ email, token, Id: newCompany._id, accountType: "company" })`
or
`json({ error: error.message })`

## Vacancy Application apis

- POST `/api/vacancy/apply/:userId/:vacancyId` createApplication

request userId, vacancyId

responce
`json({ message: "Application already exists" })`
or
`json({ message: "Application created successfully", application })`
or
`json({ message: "Server error" })`

- GET `/api/vacancy/applications/:vacancyId` getApplicationsByVacancyId

responce
`json({ applications })`
or
`json({ message: "Server error" })`

## AI apis

- POST `/api/bot/` bot responce

request (string)prompt

responce (string) result or "An error occurred."
## This section is not completed yet
- POST `/api/mic/` mic

request (mp3)audioFile

responce 1
(string) "File uploaded successfully."
or
responce 2
(json) { response }

app.use("/api/file", file);
