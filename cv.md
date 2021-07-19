# **Igor Zolotarev**

tel: +7-967-156-68-95  
email: izolotarev@hotmail.com  
location: Russia, Moscow

## **_WORKING EXPERIENCE_**

### - **Mistras Group** (USA company, work remotely from Russia)

_2010 - 2021_  
**Software Implementer**

- Implementation of the software developed in the US to Russian Oil Refineries. [PCMS Software](https://www.pcmssoftware.com/)
- SAP link integration with PCMS (Plant Condition Management Software)
- Business Intelligence Data analytics products development in Qlik Sense
- Database administration SQL Server 2017
- T-SQL queries, triggers, stored procedures
- Reporting in Crystal Reports
- On-site clients training
- Translation of documents from English to Russian; communication with the US based colleagues
- Clients technical support, troubleshooting

### - **Yamal LNG** (Moscow)

_2015 - 2016_  
**Lead Data Analyst**

- Records management of the data received from EPC-contractors and vendors
- Data extraction from Excel spreadsheets from EDMS Fusion
- Data transformation using VBA ADO and DAO recordsets
- Loading data to the Access and SQL databases
- Data quality analysis, identifying improvement options and proposals to increase efficiency of gathered business data
- Data validation using Regular Expressions patterns
- KPI metrics development
- Writing SQL queries and VBA macros
- C# Desktop Application development in Visual Studio

## **_Personal Web development Projects_**

**HSE (Human Safety Environment) Data Management System** - ASP.NET core 2 web application that manages data related to HSE violations on drilling rigs. Successfully implemented in the biggest natural gas company in Russia “Gazprom”
[http://hsedatamanagement.somee.com/](http://hsedatamanagement.somee.com/)

**Capture My Travel** - photographer booking system  
[Video Presentation](https://youtu.be/4cQl2Xc-9Q4)

## **_EDUCATION_**

### - **Cornell Institute of Business and Technology, New Zealand, Auckland**

_2017 - 2018_  
Postgraduate Diploma in Software Development
(Master’s degree equivalent in New Zealand)

- Mode of study: full-time
- GPA: 3.7

### - **Russian State University of Oil and Gas, Moscow**

_2005 - 2010_  
Bachelor of Petroleum Engineering

- Mode of study: full-time

## **_LANGUAGES_**

English – fluent; Russian – native  
IELTS (International English Language Testing System) – Score: 6.5 of 9. Level B1.

## **_PROFESSIONAL CERTIFICATES_**

- Node with React: Fullstack Web Development  
  Verification link:  
  [https://www.udemy.com/certificate/UC-b5c57163-9186-4f9d-8098-d2ce52588ddc/](https://www.udemy.com/certificate/UC-b5c57163-9186-4f9d-8098-d2ce52588ddc/)
- MCPS: Microsoft Certified Professional “Programming in C#”. 70-483 exam. Microsoft Certification ID : 12302092

## **_PROGRAMMING LANGUAGES_**

HTML, CSS, Javascript, Typescript, C#, Java, Python, Swift 5, SQL, R language, SQL, VBA

## **_Web Development Technologies_**

ASP.NET Core 2.0, Node.js, Express, React, Redux, Microservices

## **_Version Control_**

Git

## **_IDEs_**

VS code, Visual Studio 2017, Eclipse, Xcode

## **_Code snippets from my apps_**

React Authentication page: signup.js

```
import { useState, useEffect } from 'react';
import Router from 'next/router';
import useRequest from '../../hooks/use-request';

export default () => {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const { doRequest, errors } = useRequest({
    url: '/api/users/signup',
    method: 'post',
    body: {
      email,
      password
    },
    onSuccess: () => Router.push('/')
  });

  const onSubmit = async (event) => {
    event.preventDefault();

    await doRequest();
  };

  return (
    <form onSubmit={onSubmit}>
      <h1>Sign Up</h1>
      <div className="form-group">
        <label>Email Address</label>
        <input
          value={email}
          onChange={(e) => setEmail(e.target.value)}
          className="form-control"
        />
      </div>
      <div className="form-group">
        <label>Password</label>
        <input
          value={password}
          onChange={(e) => setPassword(e.target.value)}
          type="password"
          className="form-control"
        />
      </div>
      {errors}
      <button className="btn btn-primary">Sign Up</button>
    </form>
  );
};
```

Express Authentication service: signup.ts

```
import express, { Request, Response } from 'express';
import { body } from 'express-validator';
import jwt from 'jsonwebtoken';

import { validateRequest } from '../middlewares/validate-request';
import { User } from '../models/user';
import { BadRequestError } from '../errors/bad-request-error';

const router = express.Router();

router.post(
  '/api/users/signup',
  [
    body('email').isEmail().withMessage('Email must be valid'),
    body('password')
      .trim()
      .isLength({ min: 4, max: 20 })
      .withMessage('Password must be between 4 and 20 characters')
  ],
  validateRequest,
  async (req: Request, res: Response) => {
    const { email, password } = req.body;

    const existingUser = await User.findOne({ email });

    if (existingUser) {
      throw new BadRequestError('Email in use');
    }

    const user = User.build({ email, password });
    await user.save();

    // Generate JWT
    const userJwt = jwt.sign(
      {
        id: user.id,
        email: user.email
      },
      process.env.JWT_KEY!
    );

    // Store it on session object
    req.session = {
      jwt: userJwt
    };

    res.status(201).send(user);
  }
);

export { router as signupRouter };
```

# [Video Presentation](https://youtu.be/4cQl2Xc-9Q4)
