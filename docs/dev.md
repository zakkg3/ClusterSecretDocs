## Dev & Debugging.


**NOTE**: in **debug mode** object data (the secret) are sent to stdout, potentially logs are being collected by Loki / Elasticsearch or any log management platform -> **Not for production!**.

Overwirte deployment entrypoint (Kubernetes `command`) from `kopf run /src/handlers.py` to `kopf run /src/handlers.py --verbose`

## Dev: Run it in your terminal.

For development you dont want to build/push/recreate pod every time. Instead we can run the operator locally:

Once you have the config in place (kubeconfig) you can just install the requirementes (pip install /base-image/requirements.txt) and then run the operator from your machine (usefull for debbuging.)

```bash
kopf run ./src/handlers.py --verbose
```

 Make sure to have the proper RBAC in place (`kubectl apply -f yaml/00_rbac.yaml`) and also the CRD definition (`kubectl apply -f yaml/01_crd.yaml`)

### Run a dev environment.

It is recommendable to use kind for this porpuse. Also podman is great.
`make test-env`

when done:

`stop-test-env`


## Build the images

Images are built by Github actions and pushed to quay on 'git tag'.

To build this locally there is a makefile for this, you can clone this repo. edit the makefile and then run 'make all'.

You will need the base image first and then the final image.
Find the base one in the folder base-image (yes very original name)

Running just 'make' builds and push for all arch's supported. 

### Other platforms.

there is a separate github action for other platforms. This is because this needs to instal builds-essentials to be able to pip install requirements (it needs to build for some archs.)
This packages brings the image from ~50 mb to ~200mb.

All platforms are being push to the same tags. as Quay supports different platforms like DockerHub. 



# makefile

its there and updated.
