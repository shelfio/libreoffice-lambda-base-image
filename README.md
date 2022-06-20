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

execSync(`
  cd /tmp
  libreoffice7.3 --headless --invisible --nodefault --view --nolockcheck --nologo --norestore --convert-to pdf --outdir /tmp ./hello.txt
  `);
```

Other platforms are not supported yet. PRs are welcome!

## See Also

* [libreoffica-lambda-layer](https://github.com/shelfio/libreoffice-lambda-layer) - deprecated
* [aws-lambda-libreoffice](https://github.com/shelfio/aws-lambda-libreoffice) - will be updated soon to support this docker image
