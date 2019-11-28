# Node.js, Express.js, Sequelize.js and PostgreSQL RESTful API

This source code is part of [Node.js, Express.js, Sequelize.js and PostgreSQL RESTful API](https://www.djamware.com/post/5b56a6cc80aca707dd4f65a9/nodejs-expressjs-sequelizejs-and-postgresql-restful-api) tutorial.

To run locally:

* Make sure you have install and run PostgreSQL server
* Create database with the name same as in config file
* Run `npm install` or `yarn install`
* Run `sequelize db:migrate`
* Run `nodemon` or `npm start`

# input data by curl

* input student
- curl -i -X POST -H "Content-Type: application/json" -d '{ "class_name":"Class A","students": [{ "student_name":"John Doe" },{ "student_name":"Jane Doe" },{ "student_name":"Doe Doel" }] }' localhost:3000/api/classroom/add_with_students

* show by id
- curl -i -H "Accept: application/json" localhost:3000/api/classroom/2

* save or persist Lecturer, Course and Student/Course data
- curl -i -X POST -H "Content-Type: application/json" -d '{ "lecturer_name":"Kylian Mbappe","course": { "course_name":"English Grammar" }}' localhost:3000/api/lecturer/add_with_course
curl -i -X POST -H "Content-Type: application/json" -d '{ "student_id":1,"course_id": 1}' localhost:3000/api/student/add_course

# langka awal :

## instal expres
- sudo npm install express-generator -g

## buat exressjs melalui perintah berikut
- express nama-projek --view=ejs

## masuk ke dalam path projek untuk instal npm (nodejs)
- cd nama-projek && npm install

## menggunakan library sequelize untuk keperluan migrasi db
- sudo npm install -g sequelize-cli
- npm install --save sequelize

## menggunakan database postgreSQL
- npm install --save pg pg-hstore

## setting konfugurasi sequelize
- touch .sequelizerc, lalu buka file tersebut dengan perintah nano .sequelizerc
- masukan code berikut :
<code>
	const path = require('path');

	module.exports = {
	  "config": path.resolve('./config', 'config.json'),
	  "models-path": path.resolve('./models'),
	  "seeders-path": path.resolve('./seeders'),
	  "migrations-path": path.resolve('./migrations')
	};
</code> 
- ketikan perintah berikut "sequelize init" (tapa tanda kutip)
<br>
perintah tersebut akan membuat `config/config.json`, `models/index.js`, `migrations` and `seeders` folder dan file
- selanjutnya buka dan edit file config.json ada di folder config
<code>
	{
  "development": {
    "username": "postgres",
    "password": "hanacaraka",
    "database": "node_sequelize",
    "host": "127.0.0.1",
    "dialect": "postgres",
  },
  "test": {
    "username": "postgres",
    "password": "hanacaraka",
    "database": "node_sequelize",
    "host": "127.0.0.1",
    "dialect": "postgres",
  },
  "production": {
    "username": "postgres",
    "password": "hanacaraka",
    "database": "node_sequelize",
    "host": "127.0.0.1",
    "dialect": "postgres",
  }
}

</code>

## buat model dan migrasi tabel

- sequelize model:create --name Classroom --attributes class_name:string
- sequelize model:create --name Student --attributes classroom_id:integer,student_name:string
- sequelize model:create --name Lecturer --attributes lecturer_name:string
- sequelize model:create --name Course --attributes lecturer_id:integer,course_name:string
- sequelize model:create --name StudentCourse --attributes student_id:integer,course_id:integer

## jalankan migrasi
- sequelize db:migrate

- One classroom has many students and a student has one classroom
- Many students take many courses and vice-versa
- One course has one lecturer and one lecturer teach one course

Reference :
* https://www.djamware.com/post/5b56a6cc80aca707dd4f65a9/nodejs-expressjs-sequelizejs-and-postgresql-restful-api