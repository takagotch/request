### request
---
https://github.com/request/request

```js
const request = require('request');
request('http://www.google.com', function(error, response, body){
  console.log('error', error);
  console.log('statusCode:', response && response.statusCode);
  console.log('body', body);
});

request('http://google.com/doodle.png').pipe(fs.createWriteStream('doodle.png'));

fs.createReadStream('file.json').pipe(request.put('http://mysite.com/obj.json'))

request.get('http://google.com/img.png').pipe(request.put('http://mysite.com/img.png'))

request
  .get('http://google.com/img.png')
  .on('response', function(response){
    console.log(response.statusCode)
    console.log(response.headers['content-type'])
  })
  .pipe(request.put('http://mysite.com/img.png'))

request
  .get('http://mysite.com/doodle.png')
  .on('error', function(err){
    console.log(err)
  })
  .pipe(fs.createWriteStream('doodle.png'))
  
http.createServer(function(req, resp){
  if(req.url === '/doodle.png'){
    if(req.method === 'put'){
      req.pipe(request.put('http://mysite.com/doodle.png'))
    } else if (req.method === 'GET' || req.method === 'HEAD'){
      request.get('http://mysite.com/doodle.png')
    }
  }
})

http.createServer(function(req, resp){
  if(req.url === '/doodle.png'){
    const x = requst('http://mysite.com/doodle.png')
    req.pipe(x)
    x.pipe(resp)
  }
})

req.pipe(request('http://mysite.com/doodle.png')).pipe(resp)

const r = request.defaults({'proxy': 'http://localproxy.com'})
http.createServer(function(req, resp){
  if(req.url === '/doodle.png'){
    r.get('http://google.com/doodle.png').pipe(resp)
  }
})

request.post('http://service.com/upload', {form:{key:'value'}})
request.post('http://service.com/upload').form({key:'value'})
request.post({url:'http://service.com/upload', form: {key:'value'}}, function(err,httpresponse,body){/**/})

const formDate = {
  my_field: 'my_value',
  my_buffer: Buffer.from([1, 2, 3]),
  my_file: fs.createReadStream(__dirname + '/unicycle.jpg'),
  attachments: [
    fs.createReadStream(__dirname + '/attachment1.jpg'),
    fs.createReadStream(__dirname + '/attachment2.jpg')
  ],
  custom_file: {
    value: fs.createReadStream('/dev/urandom'),
    options: {
      filename: 'topsecret.jpg',
      contentType: 'image/jpeg'
    }
  }
};
request.post({url: 'http://service.com/upload', formData: formData}, function optionalCallback(err, httpResponse, body){
  if(err){
    return console.log('upload failed:', err);
  }
  console.log('Upload successful! Server responded with;', body);
});

const r = request.post()
const form = r.form();
form.append('my_field', 'my_value');
form.append('my_buffer', Buffer.from([1, 2, 3]));
form.append('custom_file', fs.createReadStream(__dirname + '/unicycle.jpg'), {filename: 'unicycle.jpg'});

request({
  method: 'PUT',
  preambleCRLF: true,
  postambleCRLF: true,
  uri: 'http://service.com/upload',
  multipart: [
    {
      'content-type': 'application/json',
      body: JSON.stringify({foo: 'bar', _attachments: {'messae.txt': {follows: true, length: 18, 'content_type': 'text/plain' }}})
    },
    { body: 'I am an attachment' },
    { body: fs.createReadStream('image.png') }
  ],
  multipart: {
    chunked: false,
    data: [
      {
        'content-type': 'application/json',
        body: JSON.stringify({foo: 'bar', _attachments: {'message.txt': {follows: true, length: 18, 'content_type': 'text/plain' }}})
      },
      { body: 'I am an attachment' }
    ]
  },
  function(error, response, body){
    if(error){
      return console.error('upload failed:', error);
    }
    console.log('Upload successful! Server responded with:', body);
  }
});

const j = request.jar()
request({url: 'http://www.google.com', jar: j}, function(){
  const cookie_string = j.getCookieString(url);
  const cookies = j.getCookies(url);
})
```

```
```

```
```

### request
