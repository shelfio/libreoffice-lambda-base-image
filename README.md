# LibreOffice Lambda Base Image

> LibreOffice 7.6 base image for Lambda Node.js 20 x86_64 to be used as a base for your own images.

## Usage

Includes CJK fonts support! 877 MB in size.

[Blog post announcement](https://vladholubiev.medium.com/running-libreoffice-in-aws-lambda-2022-edition-open-sourced-9bb0028911d8)

### Node.js 20 x86_64

> Set environment variable `HOME=/tmp` in your Lambda function.

```Dockerfile
FROM public.ecr.aws/shelf/lambda-libreoffice-base:7.6-node20-x86_64

COPY handler.js ${LAMBDA_TASK_ROOT}/

CMD [ "handler.handler" ]
```

And your `handler.js`:

```javascript
const {execSync} = require('child_process');
const {writeFileSync} = require('fs');

module.exports.handler = () => {
  writeFileSync('/tmp/hello.txt', Buffer.from('Hello World!'));

  execSync(`
  cd /tmp
  libreoffice7.6 --headless --invisible --nodefault --view --nolockcheck --nologo --norestore --convert-to pdf --outdir /tmp ./hello.txt
  `);
};
```

Other platforms are not supported yet. PRs are welcome!

## Troubleshooting

<details>
<summary>Command failed: Fatal Error: The application cannot be started. User installation could not be completed. </summary>

Set environment variable `HOME=/tmp` in your Lambda function.
</details>

## Available Tags & Versions

* `7.6-node20-x86_64`
* `7.6-node18-x86_64`
* `7.4-node16-x86_64`
* `7.3-node16-x86_64`

## See Also

* [aws-lambda-libreoffice](https://github.com/shelfio/aws-lambda-libreoffice) - utility to work with Docker version of LibreOffice in Lambda
* [libreoffica-lambda-layer](https://github.com/shelfio/libreoffice-lambda-layer) - deprecated; this is the predecessor of this image

