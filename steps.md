# Steps for Remaking Instagram

0. Clone repository, widths/heights on `html`/`body` are 100%, `margin: 0` set on `body`

1. Make body background color:

  `background-color: #fafafa;`

  Make page layout a grid, 2 rows and and 3 columns:

  ```
    .page-shell {
      width: 100%;
      height: 100%;
      display: grid;
      grid-template-columns: 1fr 615px 300px 1fr;
      grid-template-rows: 56px 1fr;
    }
  ```

  Point out that the center column's width will always be fit to its content (615px cards), the right column takes up whatever it can, fitting its content, and the left column takes up whatever space is left.

  Make topbar shell:

  ```
  .topbar {
    grid-column: 1 / span 4;
    background-color: #fff;
    border-bottom: 1px solid rgb(219, 219, 219);
  }
  ```

  Make content containers: 

  .posts-container {
    grid-column-start: 2;
  }

  .stories-container {
    grid-column-start: 3;
  }

  Add elements to DOM:
  ```
  <main class="page-shell">
    <section class="topbar"></section>
    <section class="posts-container"></section>
    <section class="stories-container"></section>
  </main>
  ```

2. Add topbar elements:

  There are multiple ways to lay this out. I'll use flexbox.
  
  ```
  .topbar-content {
    width: 915px;
    height: 100%;
    margin: 0 auto;

    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  <div class="topbar-content">
    
  </div>
  ```

  And the rest of the code:
  
  ```
  .searchbox {
    background-color: #fafafa;
    border: 1px solid #dbdbdb;
    padding: 3px 10px;
    height: 20px;
    border-radius: 5px;
  }

  .icons-box > img {
    cursor: pointer;
    width: 22px;
    height: 22px;
  }

  .icons-box > img:not(:last-child) {
    margin-right: 22px;
  }

  .profile-icon {
    border-radius: 50%;
    width: 50px;
    height: 50px;
  }

  .profile-icon.sm {
    width: 22px;
    height: 22px;
  }
  ```

  ```
  <div class="topbar-content">
  <img src="icons/iglogo.png" />
  <input placeholder="Search..." class="searchbox" type="text" />
  <div class="icons-box">
    <img src="icons/home.svg" />
    <img src="icons/paperplane.svg" />
    <img src="icons/compass.svg" />
    <img src="icons/heart.svg" />
    <img class="profile-icon sm" src="images/jvall.jpg" />
  </div>
  ```

  3. Make post shell, header:
  
  ```
    <section class="posts-container">
      <article class="post">
        <header class="post-header">
          <div class="post-account">
            <img class="profile-icon" src="images/cmaier.jpg" />
            <div>
              <p class="post-account-name">cmaier</p>
              <p class="post-account-location">Taipei Cafe</p>  
            </div>
          </div>
          <img src="icons/ellipsis.svg">
        </header>
      </article>
    </section>
  ```

  Introducing p tag, make margins 0: 

  ```
  p {
    margin: 0;
  }
  ```

  ```
  .post {
    width: 615px;
    border: 1px solid #dbdbdb;
    border-radius: 4px;
    margin-top: 20px;
  }

  .post-header {
    padding: 15px;
    display: flex;
    justify-content: space-between;
  }

  .post-account {
    display: flex;
  }

  .post-account-name {
    font-weight: bold;
    font-size: 0.9em;
  }

  .post-account-location {
    font-size: 0.8em;
  }

  .post-account > .profile-icon {
    margin-right: 10px;
  }

  .post-header > img {
    cursor: pointer;
  }
  ```

  Make some adjustments to the profile icon classes:

  ```
  .profile-icon {
    border-radius: 50%;
    width: 30px;
    height: 30px;
    border: 1px solid #dbdbdb;
  }

  .profile-icon.lg {
    width: 50px;
    height: 50px;
  }
  ```

  This is to accommodate various profile icon sizes on IG.

  1.  Write image, comment, and caption code:

  ```
  .post-image {
    width: 615px;
    height: 460px;
    object-fit: cover;
    margin-bottom: 10px;
  }

  .post-content {
    padding: 0 15px;
  }

  .post-content-line {
    margin-bottom: 3px;
    line-height: 1.4em;
  }

  .action-icons {
    width: auto;
  }

  .action-icons > img {
    margin-bottom: 10px;
    margin-right: 10px;
    width: 22px;
    height: 22px;
  }

  .bookmark-icon {
    float: right;
  }

  .post-caption {
    font-size: 0.9em;
  }

  .post-caption-name {
    font-weight: bold;
  }

  .post-timestamp {
    font-size: 0.7em;
    text-transform: uppercase;
    color: #a3a3a3;
    margin-bottom: 10px;
  }

  .write-comment-area {
    width: 100%;
    background-color: #fafafa;
    border: none;
    border-top: 1px solid #dbdbdb;
    padding: 20px 0;
    resize: none;
    font-family: inherit;
  }
  ```

  And corresponding DOM elements:

  ```
  <img class="post-image" src="images/food1.jpg" />
  <div class="post-content">
    <div class="action-icons post-content-line">
      <img src="icons/heart.svg" />
      <img src="icons/speakbubble.svg" />
      <img src="icons/paperplane.svg" />
      <img class="bookmark-icon" src="icons/bookmark.svg" />
    </div>
    <p class="post-account-name post-content-line">100 likes</p>
    <p class="post-content-line post-caption"><span class="post-caption-name">cmaier</span> red bbq pork with rice and hardboiled egg</p>  
    <p class="post-timestamp post-content-line">14 hours ago</p>
    <textarea placeholder="Write a comment..." class="write-comment-area"></textarea>
  </div>
  ```

  5. Start work on sidebar, implement logged in user:

    ```
    <section class="stories-container">
      <div class="logged-in-user">
        <img class="profile-icon lg" src="images/jvall.jpg" />
        <div>
          <p class="post-account-name">jvall</p>
          <p class="post-account-location">John Vall</p>  
        </div>
      </div>
    </section>
    ```
    ```
    .logged-in-user {
      display: flex;
      align-items: center;
      margin-top: 20px;
    }

    .logged-in-user > .profile-icon {
      margin-right: 10px;
    }

    .logged-in-username {
      margin-right: 20px;
    }
    ```

    Modify spacing and margin to accomodate new column:

    ```
    grid-template-columns: 1fr 635px 300px 1fr;
    .posts-container {
      grid-column-start: 2;
      margin-right: 20px;
    }
    ```

  6. Implement stories section

  Add stories header:

  ```
    <div class="stories">
      <div class="stories-title">
        <span class="stories-text">Stories</span>
        <span class="stories-watch-all">Watch All</span>
      </div>
    </div>
  ```

  Header base styling:
  ```
    .stories {
      border: 1px solid #dbdbdb;
      border-radius: 4px;
      padding: 10px 16px 0 16px;
      height: 230px;
    }

    .stories-title {
      display: flex;
      justify-content: space-between;
      align-items: flex-end;
      margin-bottom: 25px;
    }

    .stories-watch-all {
      font-size: 0.8em;
      font-weight: bold;
    }

    .stories-text {
      color: #a3a3a3;
      font-weight: bold;
      font-size: 0.9em;
    }
  ```

  Add specific stories DOM:
  ```
    <div class="post-account">
      <img class="profile-icon new-story" src="images/ajliptak.jpg" />
      <div>
        <p class="post-account-name">ajliptak</p>
        <p class="post-timestamp post-content-line">10 hours ago</p>
      </div>
    </div>
  ```

  Add new stories CSS:
  ```
    .profile-icon.new-story {
      border: 2px solid #e74f58;
    }
  ```

  Change logged in user padding: 
  ```
    margin: 20px 0;
  ```

  Remove post-account center styling:
  ```
  .post-account {
    display: flex;
  }
  ```

  Add padding to icon:
  ```
  .profile-icon {
      padding: 1px;
  }
  ```

  7. Add scrolling support:

  ```
    .post {
      width: 613px;
    }

    .posts-container {
      overflow-y: auto;
    }

    .stories {
      overflow-y: auto;
    }
  ```