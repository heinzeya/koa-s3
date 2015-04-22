# koa-s3
```javascript
var koa = require('koa')
var koaS3 = require('koa-s3')
var koabody = require('koa-body')({multipart: true})
var app = koa();

koaS3.set({
  keyid: '###',
  secret: '###',
  bucket: '###'
})

app.post('/images',koaBody,function*(){
  var images = this.request.body.files.images;
  var paths = yield koaS3.upload(images);
  this.body=paths;
});

app.del('/images', koaBody,function*(){
  var paths = this.request.body.fields;
  var ret = yield koaS3.remove(paths);
  this.body=ret;
});

app.listen(3000);
```
