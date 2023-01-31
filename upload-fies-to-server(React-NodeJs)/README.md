
# Upload file to server (NodeJs - React)

## Frontend code

```js
function MainScreen() {
  const [file, setFile] = useState<File>({} as File);
  const [caption, setCaption] = useState("");

  const submit = async (event: React.FormEvent<HTMLFormElement>) => {
    event.preventDefault();

    const formData = new FormData();
    formData.append("imagetest", file);
    formData.append("caption", caption);

    await axios.post("/api/upload", formData, {
      headers: { "Content-Type": "multipart/form-data" },
    }); 
  };

  return (
    <form onSubmit={submit}>
      <input
        onChange={(e: React.ChangeEvent<HTMLInputElement>) => {
          if (e.target.files) setFile(e.target.files[0]);
        }}
        type="file"
        accept="image/*"
      ></input>
      <input
        value={caption}
        onChange={(e) => setCaption(e.target.value)}
        type="text"
        placeholder="Caption"
      ></input>
      <button type="submit">Submit</button>
    </form>
  );
}
```
## Frontend code

```js
const storage = multer.diskStorage({
      destination: './public/uploads/' ,
      filename: function (req, file, cb) {
        cb(null, file.originalname)
      }
    })

app.post('/upload' , (req ,res ) => {
  upload(req, res ,err  => {
        if (err) {
              console.log('error happened')
        } else {
              console.log(req.file)
        }
  }) 
  res.sendStatus(200)
  })
```