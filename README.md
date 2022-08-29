## React Jobly Project

#### DESCRIPTION 
This is a full stack job board type project. You can see the stack outline below. This application allows you to register as a user and browse jobs and then 'apply' to them. All information is stored in a Postgres DB that has been seeded with mock data.  
This was a really good learning expreience as I had to deal with a couple of tricky items.  
The first big hurdle was figuring out how and where to use state. We typically would like to avoid placing state in App.js, but in this case, it seemed to make the most sense as we were using React Context to minimize prop drilling. With this being the case, we needed our Context Provider to be at the top the of the component architecture - thus the need for storing state at the top level.  
This seemed to work most of the time, where I ran into issues was in protecting refreshes. While testing this design pattern I ran into some timing issues. For instance, when refreshing, I have a token stored in local storage that contains the username and admin status of the current user. On refresh, the token is pulled from local storage and the user details are pulled from the DB after the username is decoded fromt the token. Most downstream components rely on the logged in status, so if a component rerenders beofre the token is checked, we run into issues. This issue was most evident in protecting certain routes from non authorized users. My solution was to just check localstoarge for a token and if it was present, then allow the user to remain on the page. This gave much more predictable results, as the API call was no longer relied upon to check auth status of the user.  
After working through issues like the one previously mentioned, I am certain that the introduction of Redux into the mix would simplify the architecture considerably. Although Im not yet an expert on Redux, I do have experience using Vuex in the VueJs ecosystem, and have employed refresh persistence using there. It is quite nice to have user info stored in one place and to not have to rely on a quick API call to retrieve user information.

#### STACK  
- React (FE) => deployed using [Surge](https://create-react-app.dev/docs/deployment/)
- Node / Express => deployed on Heroku
- Postgres => included in Heroku deployment

#### LIVE 
Click here : [JOBLY](https://automatic-tub.surge.sh/)

#### TEST USER CREDENTIALS
- username: testuser
- password: password