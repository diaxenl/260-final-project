<template>
<div class="CharacterCreator">
    <div class="heading">
      <div class="circle"></div>
      <h2>Make a character</h2>
    </div>
    <div class="add">
      <div class="form">
        <input v-model="name" placeholder="Name">
        <p>Class</p>
        <select id="professions-list" v-model="profession">
            <option value="Wizard">Wizard</option>
            <option value="Rogue">Rogue</option>
            <option value="Warrior">Warrior</option>
        </select>
        <p />
        <button @click="upload">Create</button>
      </div>
      <div class="upload" v-if="addChar">
        <h2>{{addChar.name}}</h2>
        <h2>{{addChar.profession}}</h2>
      </div>
    </div>

    <div class="heading">
      <h2>Edit/Delete a Character</h2>
    </div>
    <div class="edit">
      <div class="form">
        <input v-model="findName" placeholder="Search">
        <div class="suggestions" v-if="suggestions.length > 0">
          <div class="suggestion" v-for="s in suggestions" :key="s.id" @click="selectItem(s)">{{s.name}}
          </div>
        </div>
      </div>
      <div class="upload" v-if="findChar">
        <input v-model="findChar.name">
        <p></p>
        <img :src="findChar.path" />
      </div>
      <div class="actions" v-if="findChar">
        <button @click="deleteChar(findChar)">Delete</button>
        <button @click="editChar(findChar)">Edit</button>
      </div>
    </div>
</div>
</template>


<script>
import axios from 'axios';
export default {
  name: 'CharacterCreator',
  data() {
    return {
      name: "",
      profession: "",
      file: null,
      addChar: null,
      characters: [],
      findName: "",
      findProfession: "",
      findChar: null,
    }
  },
  created() {
    this.getChars();
  },
  computed: {
    suggestions() {
      let characters = this.characters.filter(character => character.name.toLowerCase().startsWith(this.findName.toLowerCase()));
      return characters.sort((a, b) => a.name > b.name);
    }
  },
  methods: {
    selectItem(character) {
      this.findName = "";
      this.findChar = character;
    },
    fileChanged(event) {
      this.file = event.target.files[0]
    },
      async upload() {
      try {
        let r2 = await axios.post('/api/character', {
          name: this.name,
          profession: this.profession
        });
        this.addChar = r2.data;
      } catch (error) {
        console.log(error);
      }
    },
    async getChars() {
      try {
       let response = await axios.get("/api/character");
        this.characters = response.data;
        return true;
      } catch (error) {
       console.log(error);
     }
    },
    async deleteChar(item) {
      try {
        await axios.delete("/api/character/" + item._id);
        this.findChar = null;
        this.getChars();
        return true;
      } catch (error) {
        console.log(error);
      }
    },
    async editItem(item) {
      try {
        await axios.put("/api/character/" + item._id, {
          name: this.findChar.name,
        });
        this.findChar = null;
        this.getChars();
        return true;
      } catch (error) {
        console.log(error);
      }
    },
    async editChar(character) {
      try {
        await axios.put("/api/character/" + character._id, {
          name: this.findName.name,
        });
        this.findChar = null;
        this.getChars();
        return true;
      } catch (error) {
        console.log(error);
      }
    },
  }
}
</script>

<style scoped>
.CharacterCreator {
    font-family: fantasy;
    font-size: 24px;
    display: flex;
    justify-content: center;
}


</style>