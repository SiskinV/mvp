# mvp

Task
  -My task was to make a Thrid party api that will get prices of cryptocurrencies on every hour from one service, insert it into database (preferable postgres) using Sequilize ORM, and then render it on frontend using basic React.
  -Also i was supposed to make a database table ("Coins" in my case) using migration.
  -After making it work with one service i had to make it work with another service of my choice(Adapt it for other service).
  
Work
  - I chose two apis: Nomics and Gecko
  - Then i made server running on localhost(5000),db connection, routes(Only one route),model(Coins) and controller(Coins-controller)
  
  - Database table ("Coins") was made with custom migration which i generated with sequelize migration:generate
  - Migration doesn't add automatically createdAt and updatedAt fields so i had to add those two in custom migration
  - With command (sequelize db:migrate) i created table ("Coins" in database)
  - Seeder was added later in case there is nothing in database in the beggining(cron.js launches on every 42th minute of a full hour).
  
  - Next step was getting data from service. In utils->getCriptoData.js there are two functions that do this job for us.
  - Axios was used here for fetching data from service(async await) and i used map cryMap(id->{name,price}) to extract particular data that i need (id,name and price), after making cryMap i deleted everyting in Coins table and inserted every
key,value pair of my map.It work slightly different for different services.

  - Cron job was used for making it work on every hour (->Utils->Cron)
  - In cron we choose which service we want to use (Nomics or Gecko) , they are both defined in ->Config->config.json
  
  - One route for getiing all data about cryptocurrencies http://localhost:5000/api/v1/coins/getAllCoins
  - On this call we call our async function getAllCurrencies (->Controller->coin-controller), it's a basic function for getting data from one table in database and returning data as a json with status(200) if everything works good
  
  - I used this call on frontend for getting data and then rendering it in simple table that i found on material-ui api.
 
BackEnd
  - To start backend server use command: npm start
  - If you want to set use another api you should go to -> utils -> cron and there you can set another
  - Cron does his job on every 42th minute of a full hour
  - There are two api endpoints and you can see them in ->config->config.json
  - There is one migration and one seeder.
  ` One route for getiing all data about cryptocurrencies http://localhost:5000/api/v1/coins/getAllCoins
  
FrontEnd
  - Basic table for rendering our data 
  - To start frontend use command: npm start
