const express = require('express');
const bodyParaser = require("body-parser");
const cors = require("cors");
const app = express();
const port = 3000;

app.use(cors());
app.use(bodyParaser.json());


app.get('/', async(req, res)=>{
  if(res.status(200)){
    res.send('<h1>데이터 통신 성공</h>');
  } else {
    res.status(404).send('서버 오류')
  }

})




app.post('/navebooks', async(req, res)=>{


  try {
    const title = req.body.book
    const images =[]
    for (const book of Object.values(title)){


  const naverUrl = new URL('https://openapi.naver.com/v1/search/book.json');
  naverUrl.searchParams.set('query', book);
  naverUrl.searchParams.set('display', 1);

  const options ={
    method : 'GET',
    headers : {
      'Content-Type': 'application/json',
      'X-Naver-Client-Id': 'ytaQUUoLOhwBVF3BCR1m',
      'X-Naver-Client-Secret': 'FQqOQ31UUj'
    }
  };
  const response = await fetch(naverUrl.toString(), options);

  // console.log("FetchBookImage function", response);

  if(!response.ok){
    throw new Error (`Naver API fetch failed ${response.status}`)
  }

  const data = await response.json();

  // console.log("Response URL", data.items[0]);

  images.push({
    title : data.items[0].title,
    imageURL : data.items[0].image,
    description : data.items[0].description
  })
}
  res.json(images);
// console.log("BookUrl List1", images)
  
} 

catch(error) {
  console.log("Error fetching data at Node", error)
};
})



app.listen(port, ()=>{
  console.log(`http://localhost:${port} Let get the hell` )
})
