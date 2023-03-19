# container-networking


## How to connect a Jupyter notebook in a remote container
Think of a scenario where one is tasked to build a docker container on the remote server with jupyter notebook installed. The user then needs to access that jupyter notebook from local machine for code developement. The following diagram shows how this is done.

![image](img/container-jupyter.svg)




## How to connect do a request to on flask app running on local host
First of all we have a flask app running on localhost, this is defined in app.py, where we specified `app.run(host='0.0.0.0', debug=True)`. First of all run the app in terminal 1 then in the second terminal, we then type the following to do a post request:

```
curl -X POST -H "Content-Type: application/json" -d '{"text": "May the Force be with you."}' 0.0.0.0:5000/predict
```
Note that the default port for the Flask application is 5000. 

![image](img/XXX.svg)

## How to connect do a request to on flask app in a container
The app runs when docker container spins up, as there is the following line in the dockerfile: `flask run --host=0.0.0.0 --port=5000`, This means flask app will be running on the local host(its actually the IP address of the container, but we can access it from the host that the container is running on) at port 5000.

For gunicorn, gunicorn will be listening on port 5000 with `--bind=0.0.0.0:5000`.

In another terminal, we then type the following to do a post request:

```
curl -X POST -H "Content-Type: application/json" -d '{"text": "May the Force be with you."}' 0.0.0.0:5000/predict
```

![image](img/XXX.svg)

