# python 3.9 Flask serverless lambda
Sample Serverless framework using API gateway that calls a lambda with python 3.9 with Flask.


## prerequisites
Setup the prerequisites:

- python3 and virtualenv
- nodejs: https://nodejs.org/en/download/
- servless framework: 
```
npm install -g serverless
```


## setup and use a virtualenv
See also: https://www.infoworld.com/article/3239675/virtualenv-and-venv-python-virtual-environments-explained.html

- setup a new virtualenv:
```
virtualenv venv -p python3
```

- activate the virtualenv (unix / macos):
```
. venv/bin/activate
```

or on Windows using the Command Prompt:
```
venv\Scripts\activate.bat
```

## setup flask support for lambda on serverless framework 

install (in the virtual env) the dependencies:
```
pip install Flask
pip freeze > requirements.txt
```


```
sls plugin install -n serverless-wsgi
sls plugin install -n serverless-python-requirements
```

## first time setup for serverless framework to work
on aws create a IAM user for programmatic access: https://www.serverless.com/framework/docs/providers/aws/guide/credentials/


## change service name of the new api
Change service name 'hello-world-lambda' in serverless.yml file with a new name.


## local development (on port 5050)
```
python app.py
```

## test sample endpoints 

```
curl  http://localhost:5050/ -H 'Content-Type: application/json' 
curl  http://localhost:5050/quote -H 'Content-Type: application/json' 
curl -X POST http://localhost:5050/testpost -H 'Content-Type: application/json' -d '{"message":"this is a test!"}'
```


## DEPLOY to AWS
```
export AWS_ACCESS_KEY_ID=<your-key-here>
export AWS_SECRET_ACCESS_KEY=<your-secret-key-here>
sls deploy
```

after some seconds it should prints an AWS api gateway url like this:

https://XXXXXXX.execute-api.us-east-1.amazonaws.com/

now you can access your flask apis like GET 'https://XXXXXXX.execute-api.us-east-1.amazonaws.com/quote'!

