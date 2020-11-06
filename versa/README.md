# vrnetlab / Versa FlexVNF

This is the vrnetlab Docker image for Versa FlexVNF.

Ways to connect:

- over serial console (telnet to port 5000/tcp)
- over SSH

## Building the Docker Image

Put the `.qcow2` file in this directory and run:

```
$ make docker-image
```

You should be good to go. The resulting image is called ``. You can tag
it with something else if you want, like `my-repo.example.com/vr-csr` and then
push it to your repo. The tag is the same as the version of the CSR image, so
if you have csr1000v-universalk9.16.04.01.qcow2 your final docker image will be called
vr-csr:16.04.01

Please note that you will always need to specify version when starting your
router as the "latest" tag is not added to any images since it has no meaning
in this context.

It's been tested to boot and respond to SSH with:

 * 20.2.3 (versa-flexvnf-969d704-20.2.3.qcow2)

## Usage

The default credentials are `admin/versa123`.

For convenience, tag the version that was built:
```
$ docker tag vrnetlab/vr-versa:20.2.3 vr-versa
```

Then run it as a daemon:
```
$ docker run -d --privileged --name versa1 vr-versa
```

Source the `vrnetlab.sh` (in root of project) for convenience functions:
```
$ source vrnetlab.sh
```

SSH to the router as the `admin` user:
```
$ vrssh versa1 admin
```

## Interface mapping

By default it is including six ethernet interfaces, with `eth0` as the primary management interface.

## System requirements

- CPU: 1 core
- RAM: 4GB
- Disk: ~6GB (size of the `.qcow2` image uncompressed is 5.5GB)

## FUAQ - Frequently or Unfrequently Asked Questions

### Q: Has this been extensively tested?

A: Nope. 
