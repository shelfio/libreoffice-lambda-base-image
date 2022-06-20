# LibreOffice Lambda Base Image

> LibreOffice 7.3 base image for Lambda Node.js 16 x86_64 to be used as a base for your own images.

## Usage

Includes CJK fonts support!

### Node.js 16 x86_64

```Dockerfile
FROM public.ecr.aws/shelf/lambda-libreoffice-base:7.3-node16-x86_64

COPY handler.js ${LAMBDA_TASK_ROOT}/

CMD [ "handler.handler" ]
```

Other platforms are not supported yet. PRs are welcome!
