# code.documentation
## chapter3
### Screens
- Login:

   -This page has styling that distinguish login page.
   - We used some constants to store data in our database.
        - Constant for e-mail.
        - Constant for password.
        - Constant for signup to enable users that have been registered to use their profiles.
      ```
            function Login (props,{navigation}) {
            const [email, setEmail] = useState('');
            const [password, setPassword] = useState('');



          //   const email =useState();
          //   const password =useState();


          const onSignUp = () => {
            firebase.auth().signInWithEmailAndPassword(email, password)
          }
   ```   
- Home:
  - We function (home) to coordinate styling and features of image.
    
              ```
                function Home (props,{navigation}) {


                      const {  item, horizontal, full, style, ctaColor, imageStyle } = props;

                    const imageStyles = [
                      full ? styles.fullImage : styles.horizontalImage,
                      imageStyle
                    ];
                    const cardContainer = [styles.card, styles.shadow, style];
                    const imgContainer = [styles.imageContainer,
                      horizontal ? styles.horizontalStyles : styles.verticalStyles

                    ];

                    const {currentUser,posts,payload,allPosts,users,feed} =props
                    console.log (feed)


             ```
- We used const (mapStateToProps) to store date about posts and users in database
  ```
      const mapStateToProps =(store) => ({
          currentUser: store.user.currentUser,
          posts:store.user.posts,
          following:store.user.following,
          allPosts:store.user.allPosts,

          users:store.user.users,
          feed:store.user.feed,

          // usersLoaded:store.usersState.usersLoaded,
          })
    ```      
- Profile:
  -We used some constants to store data in our database
       - Constant for setting users.
       - Constant for applying users.
  - We use some conditions to differentiate between current user or not.
 
 ```
                 const [following,setFollowing ]= useState(true);
               const [apply,setApply]=useState(true);

                const { navigation, item, horizontal, full, style, ctaColor, imageStyle } = props;

                const imageStyles = [
                  full ? styles.fullImage : styles.horizontalImage,
                  imageStyle
                ];
                const cardContainer = [styles.card, styles.shadow, style];
                const imgContainer = [styles.imageContainer,
                  horizontal ? styles.horizontalStyles : styles.verticalStyles,
                  styles.shadow
                ];
                const [user, setUser] = useState(null);
                   const {currentUser,posts,payload,photo} =props
                  console.log (currentUser)
                  console.log (posts)
                  console.log (photo)

                  console.log (props.following)
                  useEffect(() => {
                    // const { currentUser, posts } = props;

                    if (props.route.params ? props.route.params.item.id : currentUser.uid=== firebase.auth().currentUser.uid) {
                        setUser(currentUser)
                        // setUserPosts(posts)
                        // setLoading(false)
                    }
                    else {
                        firebase.firestore()
                            .collection("users")
                            .doc(props.route.params ? props.route.params.item.id : currentUser.uid)
                            .get()
                            .then((snapshot) => {
                                if (snapshot.exists) {
                                    props.navigation.setOptions({
                                        title: snapshot.data().username,
                                    })

                                    setUser({ uid:props.route.params ? props.route.params.item.id : currentUser.uid, ...snapshot.data() });
                                }
                                // setLoading(false)

                            })
                               }


                    if (props.following.map(a=>a.id).indexOf(props.route.params ? props.route.params.item.id : currentUser.uid) > -1) {
                      setFollowing(true);
                  } else {
                      setFollowing(false);
                  }
                  if (props.following.map(a=>a.id).indexOf(props.route.params ? props.route.params.item.id : currentUser.uid) > -1) {
                    setApply(true);
                } else {
                    setApply(false);
                }

                }, [props.route.params ? props.route.params.item.id : currentUser.uid, props.following])
     
