# LibreOffice Lambda Base Image

> LibreOffice 7.3 base image for Lambda Node.js 16 x86_64 to be used as a base for your own images.

## Usage

Includes CJK fonts support! 877 MB in size.

### Node.js 16 x86_64

```Dockerfile
FROM public.ecr.aws/shelf/lambda-libreoffice-base:7.3-node16-x86_64

COPY handler.js ${LAMBDA_TASK_ROOT}/

CMD [ "handler.handler" ]
```

And your `handler.js`:

```javascript
const {execSync} = require('child_process');
const {writeFileSync} = require('fs');

writeFileSync('/tmp/hello.txt', Buffer.from('Hello World!'));

execSync(`
  cd /tmp
  libreoffice7.3 --headless --invisible --nodefault --view --nolockcheck --nologo --norestore --convert-to pdf --outdir /tmp ./hello.txt
  `);
```

Other platforms are not supported yet. PRs are welcome!

## Troubleshooting

<details>
<summary>Command failed: Fatal Error: The application cannot be started. User installation could not be completed. </summary>

Set environment variable `HOME=/tmp` in your Lambda function.
</details>

## See Also

* [aws-lambda-libreoffice](https://github.com/shelfio/aws-lambda-libreoffice) - utility to work with Docker version of LibreOffice in Lambda
* [libreoffica-lambda-layer](https://github.com/shelfio/libreoffice-lambda-layer) - deprecated; this is the predecessor of this image

