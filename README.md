# How to generate a custom feed to much users
How to generate a individual feed user with Node.js, Firebase Realtime Database and Firebase Functions
> Similar with instagram feed.
> It's a trigger to Firebase Realtime Database to create a feed

### Example
```js
const globaltime=999999999999999;
                             //The ref from users create a new posts
exports.genereteFeed = functions.database.ref('/posts/{IDuser}/posts/{IDpost}')
.onCreate((snap,context)=>{

    let idUser=context.params.IDuser;
    let idPost=context.params.IDpost;
    
                                //on child_added return the list of followers one a one
    const followers = db.ref(`followers/${iduser}/followers/`)
    .on('child_added',function(params) {
      var snapShotFollower = params.val();
      var idFollower=snapShotFollower.id;
    
      //The ref where the script will create a individual feed
      var feedref=db.ref(`feed/${idFollower}/feed`);
      
      //save the data
      feedref.child(idPost).set(
        {
          idPost:idPost,
          idAuthor:idUser,
          date:globaltime-Date.now()      
      })
    });

  })
  ```
