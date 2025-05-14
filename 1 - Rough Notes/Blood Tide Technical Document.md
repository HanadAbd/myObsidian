Summary
---

Issues
--

- Poor route structure - 
  Currently the server.js structure has a separate for each html file in the page. It would be  better if there was a folder for each background stories, character pages, Location
  
- No page template - Besides the header, there isn't a consistent template for each kind of page. For example, if I wanted to make another story page, it would have to duplicate all the html and images. There should be a template and difference can be added separately e.g. the text and images.
- Looks kind of ugly- yeah just don't like any other page then the home page and story page
- Poor folder structure- basic folder groups which is nice having css and scripts within html, all the html being in 1 folder,

Dependencies
---

- Express JS - Used for a few things. Used to handle Rest API requests, running the program on a port, as well as setting up the file, public as the default folder for the html and css and other assets.
- node- Used to run the actual program locally. So the website can run off the browser. Probably isn't strictly necessary

Changes for next time
--

- Better api route directory 
- Try hosting the images and text elsewhere instead of on the client side
- More easier to maintain and manage CSS
- Do the working figma board first before jumping in to the website code.
- Add a asset profile system for each character and location which would be both reflected in the url and code e.g. characters/sam/story?=she0x20came0x20the0x20woods (Something like that)
- Try using angular or react JS instead of a traditional node file struct (Very optional and really not too important)