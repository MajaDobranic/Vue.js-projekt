<template>

      <div class="container">
        <div class="slider-container">
          <input
            id="price-slider"
            type="range"
            min="2.6"
            max="20"
            v-model="priceRange"
            @input="updateFilteredMenuItems"
          />
          <button class="random-btn" @click="displayRandomItem()"><i class="fa-solid fa-shuffle"></i>choose random item</button>

          <div class="progress-bar" :style="{ width: priceRange * 5 + '%' }"></div>
          
        </div>
      </div>

     <div class="container2">
        <input
        id="search-input"
        type="text"
        v-model="searchTerm"
        placeholder="Search by name"
        @keyup.enter="filteredMenu()"
        />
     </div>

    <div class="btn-container">
      <button
        class="filter-btn"
        type="button"
        v-for="category in categories"
        :key="category"
        @click="filterMenuItems(category)"
      >
        {{ category }}
      </button>
    </div>
  
    <div class="section-center">
      <article class="menu-item" v-for="item in filteredMenuItems" :key="item.id">
        <img :src="item.img" class="photo" :alt="item.title" />
        <div class="item-info">
          <header>
            <h4>{{ item.title }}</h4>
            <h4 class="price">{{ item.price }}€</h4>
          </header>
          <p class="item-text">
            {{ item.desc }}
          </p>
        </div>
      </article>
    </div>
    <div class="btn-container2">
      <button class="btt-btn" @click="scrollToTop">Back to Top</button>
    </div>
</template>

<script>
export default {
  data() {
    return {
      menu: [
        {
          id: 1,
          title: "chicken cheese pasta",
          category: "lunch",
          price: 6.30,
          img: "./slike/slika1.jpg",
          desc: `Lorem ipsum dolor sit amet consectetur adipisicing elit. Delectus, dicta. Deserunt, optio! Perspiciatis odit exercitationem maiores autem ullam facere quod.`,
        },
        {
        id: 2,
        title: "avocado toast",
        category: "breakfast",
        price: 4.20,
        img: "./slike/slika2.jpg",
        desc: `Lorem ipsum dolor sit amet consectetur adipisicing elit. Delectus, dicta. 
        Deserunt, optio! Perspiciatis odit exercitationem maiores autem ullam facere quod.`,
      },
      {
        id: 3,
        title: "steak tartare",
        category: "lunch",
        price: 13.12,
        img: "./slike/slika3.jpg",
        desc: `Lorem ipsum dolor sit amet consectetur adipisicing elit. Delectus, dicta. 
        Deserunt, optio! Perspiciatis odit exercitationem maiores autem ullam facere quod.`,
      },
      {
        id: 4,
        title: "chia pudding",
        category: "breakfast",
        price: 4.60,
        img: "./slike/slika4.jpg",
        desc: ` Lorem ipsum dolor sit amet consectetur adipisicing elit. Delectus, dicta. 
        Deserunt, optio! Perspiciatis odit exercitationem maiores autem ullam facere quod.`,
      },
      {
        id: 5,
        title: "cheesecake",
        category: "dessert",
        price: 2.60,
        img: "./slike/slika5.jpg",
        desc: `Lorem ipsum dolor sit amet consectetur adipisicing elit. Delectus, dicta. 
        Deserunt, optio! Perspiciatis odit exercitationem maiores autem ullam facere quod. `,
      },
      {
        id: 6,
        title: "tofu ramen noodles",
        category: "lunch",
        price: 10.25,
        img: "./slike/slika6.jpg",
        desc: `Lorem ipsum dolor sit amet consectetur adipisicing elit. Delectus, dicta. 
        Deserunt, optio! Perspiciatis odit exercitationem maiores autem ullam facere quod.`,
      },
      {
        id: 7,
        title: "spicy chicken chowmain",
        category: "lunch",
        price: 9.60,
        img: "./slike/slika7.jpg",
        desc: `Lorem ipsum dolor sit amet consectetur adipisicing elit. Delectus, dicta. 
        Deserunt, optio! Perspiciatis odit exercitationem maiores autem ullam facere quod. `,
      },
      {
        id: 8,
        title: "chili con carne",
        category: "lunch",
        price: 8.90,
        img: "./slike/slika8.jpg",
        desc: `Lorem ipsum dolor sit amet consectetur adipisicing elit. Delectus, dicta. 
        Deserunt, optio! Perspiciatis odit exercitationem maiores autem ullam facere quod. `,
      },
      {
        id: 9,
        title: "blueberry oatmeal",
        category: "breakfast",
        price: 4.60,
        img: "./slike/slika9.jpg",
        desc: `Lorem ipsum dolor sit amet consectetur adipisicing elit. Delectus, dicta. 
        Deserunt, optio! Perspiciatis odit exercitationem maiores autem ullam facere quod.`,
      },
      {
        id: 10,
        title: "chocolate brownie",
        category: "dessert",
        price: 2.60,
        img: "./slike/slika10.jpg",
        desc: `Lorem ipsum dolor sit amet consectetur adipisicing elit. Delectus, dicta. 
        Deserunt, optio! Perspiciatis odit exercitationem maiores autem ullam facere quod.`,
      },
        
      ],
      searchTerm: "",
      categories: ["all", "lunch", "breakfast", "dessert"],
      filteredMenuItems: [], // Updated property name
      priceRange: 0,
    };
  },

  methods: {

    filteredMenu() {
      const searchTerm = this.searchTerm.toLowerCase();
      if (searchTerm === "") {
        return this.menu;
      } else {
        this.filteredMenuItems = this.menu.filter((menuItem) =>
          menuItem.title.toLowerCase().includes(searchTerm)
        );
      }
    },

    filterMenuItems(category) {
      if (category === "all") {
        this.filteredMenuItems = this.menu; // Update property assignment
      } else {
        this.filteredMenuItems = this.menu.filter(
          (menuItem) => menuItem.category === category
        );
      }
    },

    updateFilteredMenuItems() {
      const priceRange = this.priceRange;
      if (priceRange === 0) {
        this.filteredMenuItems = this.menu;
      } else {
        this.filteredMenuItems = this.menu.filter(
          (menuItem) => menuItem.price <= priceRange
        );
      }
    },

    scrollToTop() {
      window.scrollTo({
        top: 0,
        behavior: "smooth",
      });
    },

    displayRandomItem() {
      const randomIndex = Math.floor(Math.random() * this.menu.length);
      const randomItem = this.menu[randomIndex];
      this.filteredMenuItems = [randomItem];
    },
    
  },
  mounted() {
    this.filteredMenuItems = this.menu; // Update property assignment
  },
};
</script>
