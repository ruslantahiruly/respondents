<template>
  <header class="header">
    <div class="container">
      <div class="row is-space-between">
        <form action="" class="search col-7">
          <input type="text" class="search__input" placeholder="Поиск по системе">
          <button name="button" class="search__button search-button" aria-label="Поиск по системе">
            <svg viewBox="0 0 24 24" preserveAspectRatio="xMidYMid meet" focusable="false" class="search-button__icon">
              <g class="style-scope yt-icon">
                <path d="M15.5 14h-.79l-.28-.27C15.41 12.59 16 11.11 16 9.5 16 5.91 13.09 3 9.5 3S3 5.91 3 9.5 5.91 16 9.5 16c1.61 0 3.09-.59 4.23-1.57l.27.28v.79l5 4.99L20.49 19l-4.99-5zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5 14z" class="style-scope yt-icon"></path>
              </g>
            </svg>
          </button>
        </form>
        <div class="profile">
          <div class="profile__photo profile-photo mr-1">
            <img src="/user.png" alt="Пользователь" class="profile-photo__img">
          </div>
          <div class="profile__text profile-text">
            <span class="profile-text__name">Alexander C.</span>
            <span class="profile-text__role">Администратор</span>
          </div>
        </div>
      </div>
    </div>
  </header>
</template>

<style lang="scss" scoped>
.header {
  padding: 2rem;
}

.search {
  display: flex;
  justify-content: space-between;
  max-width: 550px;
}

.search__input {
  border: 2px solid $border;
  color: $secondary;
  border-radius: 7px 0 0 7px;
  border-right: none;
  outline: none;
  flex-basis: 90%;
  padding: 0 1rem;
  height: 3.2rem;
  line-height: 3.2rem;
}

.search__button {
  flex-basis: 10%;
  height: 3.2rem;
  border: 2px solid $border;
  border-left: none;
  border-radius: 0 7px 7px 0;
  background: #fff;
  cursor: pointer;
}

.search-button__icon {
  width: 1.35rem;
  height: 1.35rem;
  color: #6e6e6e;
  opacity: .5;
  vertical-align: middle;
  transition: all .1s;
}

.profile {
  display: flex;
  align-items: center;
  cursor: pointer;
}

.profile__photo {
  border-radius: 50%;
  overflow: hidden;
  width: 50px;
  height: 50px;
  background: #ccc;
}

.profile-photo__img {
  height: 100%;
}

.profile-text__name {
  display: block;
  font-weight: 700;
  font-size: 1.2rem;
}

.profile-text__role {
  display: block;
  color: $secondary;
  font-size: .9rem;
}
</style>
