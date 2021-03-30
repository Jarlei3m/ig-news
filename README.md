<h1 align="center">
    <p>ig.news</p>
    <img alt="ig-news avatar" src="https://github.com/Jarlei3m/ig-news/blob/main/public/images/avatar.svg" width="80" />
    <br>
</h1>

<h4 align="center">
  A blog to get updated news about React with a paid subscription plan.
</h4>

<p align="center">

  <img alt="GitHub top language" src="https://img.shields.io/github/languages/top/Jarlei3m/ig-news?style=plastic">

  <img alt="GitHub language count" src="https://img.shields.io/github/languages/count/Jarlei3m/ig-news?style=plastic">

  <img alt="Repository size" src="https://img.shields.io/github/repo-size/jarlei3m/ig-news?style=plastic">
  <a href="https://github.com/jarlei3m/ig-news/commits/master">
    <img alt="GitHub last commit" src="https://img.shields.io/github/last-commit/jarlei3m/ig-news?style=plastic">
  </a>

  <a href="https://github.com/jarlei3m/ig-news/issues">
    <img alt="Repository issues" src="https://img.shields.io/github/issues/jarlei3m/Comfy-Sloth-Store-ReactJS?style=plastic">
  </a>
  
  <a href="https://github.com/Jarlei3m/ig-news/blob/master/LICENSE">
    <img alt="GitHub" src="https://img.shields.io/github/license/jarlei3m/ig-news?style=plastic">
  </a>
</p>

<p align="center">
  <a href="#sparkles-technologies">Technologies</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#information_source-how-to-use">How To Use</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#memo-license">License</a>
</p>

<p align="center">
  <img alt="GitHub top language" src="https://github.com/Jarlei3m/ig-news/blob/main/public/images/ignews-gif.gif">
</p>

## :sparkles: Technologies

This project was developed at the [Rocketseat - Ignite course](https://rocketseat.com.br/) with the following technologies:

-  [React.js](https://reactjs.org/)
-  [TypeScript](https://www.typescriptlang.org/)
-  [Next.js](https://nextjs.org/)
-  [Scss](https://sass-lang.com/)
-  [Faunadb](https://fauna.com/)
-  [Prismic](https://prismic.io/)
-  [Stripe](https://stripe.com/)
-  [NextAuth](https://next-auth.js.org/)
-  [Axios](https://github.com/axios/axios)
-  [React-Icons](https://react-icons.github.io/react-icons/)
-  [VS Code][vc]

## :information_source: How To Use

Before you clone this repository, you gonna need to follow these steps:
 ### Faunadb: 
 - Access [Faunadb](https://fauna.com/) and create an account, 
 - Click on ```New Database```, you can call it ignews but it's not a must ,
 - After database has been created, you need to create 2 Collections that must must must have the names: ```subscriptions``` and ```users```,
 - Now you need to create 5 Index for this database, click on New Index and for each one fill the fields as follow:
 
    1) ##### Index Name: ```subscription_by_id```  |  Source Collection: ```subscriptions```  |  Terms: ```data.id```
    2) ##### Index Name: ```subscription_by_status```  |  Source Collection: ```subscriptions```  |  Terms: ```data.status```
    3) ##### Index Name: ```subscription_by_user_ref```  |  Source Collection: ```subscriptions```  |  Terms: ```data.userId```
    4) ##### Index Name: ```user_by_email```  |  Source Collection: ```users```  |  Terms: ```data.email``` | Unique checkbox: ```checked```
    5) ##### Index Name: ```user_by_stripe_customer_id```  |  Source Collection: ```users```  |  Terms: ```data.stripe_customer_id```
  
 - In Security tab, click on ```New Key```, select 'Role' as Admin and then Save. Get your Key's secret and put on your ```.env.local``` (you must create this file on the root of the project): ```FAUNADB_KEY=whatever-is-your-secret-key```

### Stripe: 
 - Access [Stripe](https://stripe.com/) and create an account, 
 - On tab Product, click on '+ Add a test product' button, and do as follow:
 
    1) ##### Name: ```Subscription```  |  Pricing model: ```standart pricing```  |  Price: ```9.90 USD Recurring``` | Billing period: ```Monthly```

 - Then, click on Save product and get API ID of the price, which will be something like ```price_1IZfs8FF8LwLlEROOCvQVX2S```, now you need to replace in the function getStaticProps located on ```/src/pages/index.tsx``` the current api id for your new API ID.
 - On tab Developers, get your secret key and save on your ```.env.local``` file as ```STRIPE_API_KEY=put_your_SECRET_KEY_here```.
 - On tab Settings -> checkout settings -> configure webhooks -> click on ```instal CLI```button and follow the instructions acoording to your OS.
 - After stripe has been installed, on your terminal ```$ stripe login``` -> Press Enter -> stripe page will open, click ```Allow Access```.
 - Now, to start listen the webhooks, on your terminal ```$ stripe listen --forward-to localhost:3000/api/webhooks ``` a message with your webhook sign secret will be shown, copy and save on ```.env.local``` as ```STRIPE_WEBHOOK_SECRET=put_your_WEBHOOK_SECRET_here``` 
 - For the last, on ```.env.local``` save ```STRIPE_SUCCESS_URL=http://localhost:3000/posts``` and ```STRIPE_CANCEL_URL=http://localhost:3000```.
 
 ### Prismic: 
 - Access [Prismic](https://prismic.io/) and create an account, 
 - Click on ```Create Repository```, and do as follow:
 
    1) ##### Repository name: ```Any name you want```  |  role/job title: ```Developer```  |  Technology: ```Next.js``` | Avalilable plan: ```Free```

 - On tab Custom type, select Repeatable Type, and name as 'Publication',
 - Get UID box, and drop it on the top, put name as 'UID',
 - Bellow UID box, drop the Title box with name 'Title, and select only 'h1' box,
 - And bellow Title bopx, drop the 'Rich Text' box, name it 'Content', check 'Allow target blank for links'
 - And it´s done, now you can create posts on document tab, save and publish.
 - On settings -> API & Security, on Repository security, select API access as ```Private API - Req...```, then click 'Change API visibility',
 - On Generate an Access Token, fill the Apllicaiton name as you want and click on 'Add this application'.
 - Now you have the Permanent access token, copy the 'access to master' and save on ```.env.local``` as ```PRISMIC_ACCESS_TOKEN=put_your_PERMANENT_TOKEN_here``` 
 
 ### Github: 
 - Click on Settings -> Developer settings -> OAuth Apps, click on ```New Oauth App``` button, and fill the fields as follow:
 
    1) ##### Application Name: ```Any name you want``` | Homepage URL: ```http://localhost:3000``` | Authorization URL: ```http://localhost:3000/api/auth/callback```
    
 - Then, click on register. 
 - Get the Client ID and Client secrets and save on ```.env.local``` as ```GITHUB_CLIENT_ID=put_your_CLIENT_ID_here``` and ```GITHUB_CLIENT_SECRET=put_your_CLIENT_SECRET_here```.
 
To clone and run this application, you'll need [Git](https://git-scm.com), [Node.js v10][nodejs] or higher installed on your computer. From your command line:

```bash

# Clone this repository
$ git clone https://github.com/jarlei3m/ig-news

# Go into the repository
$ cd ig-news

# Install dependencies
$ yarn

# Listen the webhooks
$ stripe listen --forward-to localhost:3000/api/webhooks  

# Run the app
$ yarn dev
```

To view the project you can open `http://localhost:3000` on your browser.

## :memo: License
This project is under the MIT license. See the [LICENSE](https://github.com/Jarlei3m/ig-news/blob/master/LICENSE) for more information.

---

Made with ♥ by Járlei Rodrigues :wave: [Get in touch!](https://www.linkedin.com/in/jarleirodrigues/)

[vc]: https://code.visualstudio.com/
[nodejs]: https://nodejs.org/
