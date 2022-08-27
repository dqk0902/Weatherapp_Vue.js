<template>
  <nav>
    <div class="menu-item">
      <div v-for="m in menu" :key="m.title">
        <a v-if="m.link" :href="m.link">{{ m.title }}</a>
        <input class="menu-item1" type="radio" name="input-menu" id="menu1" />
        <label for="menu1" @click="isOpen = !isOpen">{{ m.title }}</label>
        <ul class="menu-item-children" v-if="isOpen">
          <li v-for="c in m.children" :key="c.title" class="menu-item">
            <a href="c.link">{{ c.title }}</a>
          </li>
        </ul>
      </div>
    </div>
    <div class="menu-item">
      <div v-for="m in contact" :key="m.title">
        <a v-if="m.link" :href="m.link">{{ m.title }}</a>
        <input class="menu-item1" type="radio" name="input-menu" id="menu2" />
        <label for="menu2" @click="isOpen = !isOpen">{{ m.title }}</label>
        <ul class="menu-item-children" v-if="isOpen">
          <li v-for="c in m.children" :key="c.title" class="menu-item">
            <a href="c.link">{{ c.title }}</a>
          </li>
        </ul>
      </div>
    </div>
    <div class="menu-item">
      <div v-for="m in home" :key="m.title">
        <a v-if="m.link" :href="m.link">{{ m.title }}</a>
        <input class="menu-item1" type="radio" name="input-menu" id="menu3" />
        <label for="menu3" @click="isOpen = !isOpen">{{ m.title }}</label>
        <ul class="menu-item-children" v-if="isOpen">
          <li v-for="c in m.children" :key="c.title" class="menu-item">
            <a href="c.link">{{ c.title }}</a>
          </li>
        </ul>
      </div>
    </div>
    <div class="menu-item">
      <div v-for="m in service" :key="m.title">
        <a v-if="m.link" :href="m.link">{{ m.title }}</a>
        <input class="menu-item1" type="radio" name="input-menu" id="menu4" />
        <label for="menu4" @click="isOpen = !isOpen">{{ m.title }}</label>
        <ul class="menu-item-children" v-if="isOpen">
          <li v-for="c in m.children" :key="c.title" class="menu-item">
            <a href="c.link">{{ c.title }}</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>
<style>
.menu-item1 {
  display: none;
}
.menu-item-children {
  position: absolute;
  background-color: #222;
  top: calc(100% + 18px);
  left: 50%;
  transform: translateX(-50%);
  width: max-content;
  border-radius: 0px 0px 16px 16px;
}
.menu-item1:checked ~ .menu-item-children {
  display: block;
}
.menu-item-children {
  display: none;
}
</style>
<script>
export default {
  name: "nav-bar",

  data() {
    return {
      isOpen: false,
      menu: [
        {
          title: "MENU",
          link: false,
          children: [
            {
              title: "About Us",
              link: "#",
            },
            {
              title: "Products",
              link: "#",
            },
            {
              title: "Manager",
              link: "#",
            },
          ],
        },
      ],
      contact: [
        {
          title: "CONTACT",
          link: false,
          children: [
            {
              title: "Administrator",
              link: "#",
            },
            {
              title: "Phone Call",
              link: "#",
            },
            {
              title: "Social Media",
              link: "#",
            },
          ],
        },
      ],
      home: [
        {
          title: "HOME",
          link: false,
          children: [
            {
              title: "About Us",
              link: "#",
            },
            {
              title: "Manager",
              link: "#",
            },
            {
              title: "Love Story",
              link: "#",
            },
          ],
        },
      ],
      service: [
        {
          title: "SERVICE",
          link: false,
          children: [
            {
              title: "Web",
              link: "#",
            },
            {
              title: "Design",
              link: "#",
            },
            {
              title: "Video",
              link: "#",
            },
          ],
        },
      ],
    };
  },
};
</script>

<style>
nav {
  display: flex;
  align-items: center;
  justify-content: center;
}
nav .menu-item {
  color: white;
  padding: 10px 20px;
  position: relative;
  text-align: center;
  border-bottom: 3px solid transparent;
  display: flex;
  transition: 0.4s;
}
nav .menu-item.active,
nav .menu-item:hover {
  background-color: #444;
  border-bottom-color: #ff5858;
}
nav .menu-item a {
  color: inherit;
  text-decoration: none;
}
</style>
