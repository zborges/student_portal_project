<template>
  <div class="home">
    <div id="student-data">
      <!-- v-for/v-bind image link {{student.photo}}-->
      <img src="" alt="" />
      <h3>{{ student.first_name }} {{ student.last_name }}</h3>
      <!-- <h3>First Name</h3> -->
      <h3></h3>
      <!-- <h3>Last Name</h3> -->
      <p>{{ student.email }}</p>
      <!-- <p>Email</p> -->
      <p>{{ student.phone }}</p>
      <p>Phone Number:</p>
      <!-- <p>{{student.photo}}</p> -->
      <p>Photo:</p>
      <!-- <p>{{student.bio}}</p> -->
      <p>Bio:</p>
      <!-- <p>{{student.linkedin_url}}</p> -->
      <p>Linkedin URL:</p>
      <!-- <p>{{student.twitter_handle}}</p> -->
      <p>Twitter:</p>
      <!-- <p>{{student.website_url}}</p> -->
      <p>Website:</p>
      <!-- <p>{{student.resume_url}}</p> -->
      <p>Resume:</p>
      <!-- <p>{{student.github_url}}</p> -->
      <p>Github:</p>
      <!-- <p>{{student.bio}}</p> -->
      <button type="button" v-on:click="editStudentModal">Edit</button>
      <dialog id="student-details">
        <form method="dialog">
          <h1>Edit Your Info</h1>
          <p>
            First Name:
            <input type="text" v-model="student.first_name" />
          </p>
          <p>
            Last Name:
            <input type="text" v-model="student.last_name" />
          </p>
          <p>
            Email:
            <input type="text" v-model="student.email" />
          </p>
          <p>
            Phone:
            <input type="text" v-model="student.phone" />
          </p>
          <p>
            Bio:
            <input type="text" v-model="student.bio" />
          </p>
          <p>
            Linkedin Url:
            <input type="text" v-model="student.linkedin_url" />
          </p>
          <p>
            Twitter:
            <input type="text" v-model="student.twitter_handle" />
          </p>
          <p>
            Personal Website:
            <input type="text" v-model="student.website_url" />
          </p>
          <p>
            Resume Url:
            <input type="text" v-model="student.resume_url" />
          </p>
          <p>
            Github_url:
            <input type="text" v-model="student.github_url" />
          </p>
          <p>
            Photo:
            <input type="text" v-model="student.photo" />
          </p>
          <button v-on:click="updateStudent(student)">Update</button>
          <button>Close</button>
        </form>
      </dialog>
    </div>

    <div id="student-experiences">
      <h3>Experience:</h3>
      <div id="experiences-list" v-for="experience in experiences" :key="experience.id">
        <h4>{{ experience.company_name }}| {{ experience.job_title }}</h4>
        <p>
          <strong>{{ experience.start_date }} - {{ experience.end_date }}</strong>
        </p>
        <p>{{ experience.details }}</p>
        <button type="button" v-on:click="editExperienceModal">Edit</button>
      <dialog id="experience-details">
        <form method="dialog">
          <h1>Edit Your Experience</h1>
          <p>
            Start Date:
            <input type="text" v-model="currentExperience.start_date" />
          </p>
          <p>
            End Date:
            <input type="text" v-model="currentExperience.end_date" />
          </p>
          <p>
            Job Title:
            <input type="text" v-model="currentExperience.job_title" />
          </p>
          <p>
            Company Name:
            <input type="text" v-model="currentExperience.company_name" />
          </p>
          <p>
            Details:
            <input type="text" v-model="currentExperience.details" />
          </p>
          <button v-on:click="updateExperience(currentExperience)">Update</button>
          <button v-on:click="destroyExperience(currentExperience)">Delete</button>
          <button>Close</button>
        </form>
      </dialog>
      </div>
      <button v-on:click="createWindow">Add Experience</button>
      <dialog id="create-experience-window">
        <form method="dialog">
          <h1>New Experience</h1>
          <div class="form-group">
            <label>Start Date:</label>
            <input type="text" class="form-control" v-model="experiences.start_date" />
          </div>
          <div class="form-group">
            <label>End Date:</label>
            <input type="text" class="form-control" v-model="experiences.end_date" />
          </div>
          <div class="form-group">
            <label>Job Title:</label>
            <input type="text" class="form-control" v-model="experiences.job_title" />
          </div>
          <div class="form-group">
            <label>Company Name:</label>
            <input type="text" class="form-control" v-model="experiences.company_name" />
          </div>
          <div class="form-group">
            <label>Details:</label>
            <input type="text" class="form-control" v-model="experiences.details" />
          </div>
          <button v-on:click="createExperience()">Submit</button>
          <button>close</button>
        </form>
      </dialog>
      
    </div>

    <div class="student-education">
      <button v-on:click="showEducation()">Education Input</button>
      <h3>Education:</h3>
      <div v-for="education in education_lists" :key="education.id">
        <h3>{{ education.university }} | {{ education.degree }}</h3>
        <p>
          <strong>{{ education.start_date }} - {{ education.end_date }}</strong>
        </p>
        <p>{{ education.details }}</p>
      </div>
      <button v-on:click="showEducation()">Add Education</button>
      <dialog id="education-details">
        <form method="dialog">
          <h1>Education</h1>
          <div class="form-group">
            <label>Start Date:</label>
            <input type="text" class="form-control" v-model="start_date" />
          </div>
          <div class="form-group">
            <label>End Date:</label>
            <input type="text" class="form-control" v-model="end_date" />
          </div>
          <div class="form-group">
            <label>Degree:</label>
            <input type="text" class="form-control" v-model="degree" />
          </div>
          <div class="form-group">
            <label>University Name:</label>
            <input type="text" class="form-control" v-model="university" />
          </div>
          <div class="form-group">
            <label>Details:</label>
            <input type="text" class="form-control" v-model="details" />
          </div>
          <input type="submit" class="btn btn-primary" value="Submit" />
          <button>Close</button>
        </form>
      </dialog>
    </div>

    <div id="student-capstone">
      <button v-on:click="createCapstoneWindow">Add Capstone</button>
      <dialog id="create-capstone-window">
        <h3>Capstone:</h3>
        <form method="dialog">
          <div class="form-group">
            <label>Name:</label>
            <input type="text" class="form-control" v-model="name" />
          </div>
          <div class="form-group">
            <label>Description:</label>
            <input type="text" class="form-control" v-model="description" />
          </div>
          <div class="form-group">
            <label>URL:</label>
            <input type="text" class="form-control" v-model="url" />
          </div>
          <div class="form-group">
            <label>Screenshot:</label>
            <input type="text" class="form-control" v-model="screenshot" />
          </div>
          <button v-on:click="createCapstone()">Submit</button>
          <button>close</button>
        </form>
      </dialog>
      <div id="capstone-list" v-for="capstone in capstones" :key="capstone.id">
        <ul>
          <li>
            {{ capstone.name }}
          </li>
          <button v-on:click="destroyCapstone(capstone)"></button>
        </ul>
        <!-- Capstone edit dialog and button -->
        <button v-on:click="editCapstoneWindow">Edit Capstone</button>
        <dialog id="edit-capstone-window">
          <h3>Edit Capstone:</h3>
          <form method="dialog">
            <div class="form-group">
              <label>Name:</label>
              <input type="text" class="form-control" v-model="name" />
            </div>
            <div class="form-group">
              <label>Description:</label>
              <input type="text" class="form-control" v-model="description" />
            </div>
            <div class="form-group">
              <label>URL:</label>
              <input type="text" class="form-control" v-model="url" />
            </div>
            <div class="form-group">
              <label>Screenshot:</label>
              <input type="text" class="form-control" v-model="screenshot" />
            </div>

            <button v-on:click="updateCapstone()">Update</button>
            <button>close</button>
          </form>
        </dialog>
      </div>
    </div>

    <div id="student-skills">
      <h3>Skills:</h3>
      <form v-on:submit.prevent="createSkills()">
        <input v-model="new_s" type="text" id="skill-input" placeholder="CRUD Apps, Ruby, etc.¸" />
        <button type="submit">Add Skill</button>
      </form>
      <div id="skills-list" v-for="skill in orderdSkills" :key="skill.id">
        <ul>
          <li>
            {{ skill.name }}
            <button v-on:click="destroySkill(skill)">Delete</button>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
// import func from "vue-editor-bridge";
export default {
  data: function () {
    return {
      student: {},
      skills: {},
      capstones: {},
      name: "",
      description: "",
      url: "",
      screenshot: "",
      experiences: {
        start_date: "",
        end_date: "",
        job_title: "",
        company_name: "",
        details: "",
      },
      currentExperience: {},
      // education experience data
      start_date: "",
      end_date: "",
      degree: "",
      university: "",
      details: "",

      skills_list: ["alphabet", "soup"],
      new_skill: "",
      errors: [],

      // each variable above will need data here!
    };
  },
  computed: {
    orderdSkills: function () {
      var skills_array = this.skills_list;
      return skills_array.sort((a, b) => (a.name > b.name ? 1 : -1));
    },
  },
  mounted: function () {
    this.showStudent();
    this.showSkills();
  },
  methods: {
    // incomplete/ need routes to correctly create these methods

    showStudent: function () {
      axios.get("/api/students/" + this.$route.params.id).then((response) => {
        console.log(response.data);
        this.student = response.data;
      });
    },
    showSkills: function () {
      axios.get("/api/skills/").then((response) => {
        console.log(response.data);
        this.skills_list = response.data;
      });
    },
    showEducations: function () {
      axios.get("/api/education/").then((response) => {
        console.log(response.data);
        this.education_list = response.data;
      });
    },
    showCapstones: function () {
      axios.get("/api/capstones/").then((response) => {
        console.log(response.data);
        this.capstones_list = response.data;
      });
    },
    showExperiences: function () {
      axios.get("/api/experiences/").then((response) => {
        console.log(response.data);
        this.experiences = response.data;
      });
    },
    createCapstone: function () {
      console.log("Creating your capstone info!");
      var params = {
        name: this.name,
        description: this.description,
        url: this.url,
        screenshot: this.screenshot,
      };
      axios
        .post("/api/capstone/" + this.student.id, params)
        .then(() => {
          // this.$router.push("/profile");
        })
        .catch((error) => console.log(error.response));
    },
    updateCapstone: function (capstone) {
      console.log("Updating capstone");
      var params = {
        name: capstone.name,
        description: capstone.description,
        url: capstone.url,
        screenshot: capstone.screenshot,
      };
      axios
        .patch("/api/capstone/" + this.student.id, params)
        .then(() => {
          // this.$router.push("/capstones/" + this.capstone.id);
        })
        .catch((error) => console.log(error.response));
    },
    destroyCapstone: function (capstone) {
      axios.delete("/api/capstone/" + capstone.id).then(() => {
        console.log("Destroyed");
        // this.$router.push("/students");
      });
    },
    createSkill() {
      var params = {
        skill_name: this.new_skill,
      };
      axios
        .post("/api/skills", params)
        .then((response) => {
          console.log("skill being added...", response.data);
          this.skills_list.unshift(response.data);
        })
        .catch((error) => {
          console.log(error.response);
          this.errors = error.response.data.errors;
        });
      this.new_skill = "";
      // console.log(`"${this.new_skill} being added..."`);
      // this.skills_list.unshift(this.new_skill);
      // this.new_skill = "";
    },
    destroySkill(skill) {
      axios.delete("/api/skills/" + skill.id).then((response) => {
        console.log("skill being deleted...", response.data);
        var index = this.skills_list.indexOf(skill);
        this.skills_list.splice(index, 1);
      });
      // console.log("skill being deleted...");
      // var index = this.skills_list.indexOf(skill);
      // this.skills_list.splice(index, 1);
    },
    updateStudent: function (student) {
      let params = {
        first_name: student.first_name,
        last_name: student.last_name,
        email: student.email,
        phone: student.phone,
        bio: student.bio,
        linkedin_url: student.linkedin_url,
        twitter_handle: student.twitter_handle,
        website_url: student.website_url,
        resume_url: student.resume_url,
        github_url: student.github_url,
        photo: student.photo,
      };
      axios.patch("/api/students/" + student.id, params).then((response) => {
        console.log("Success!", response.data);
      });
    },
    editStudentModal: function () {
      document.querySelector("#student-details").showModal();
    },
    createEducation: function () {
      console.log("Creating Education info");
      var params = {
        startDate: this.start_date,
        endDate: this.end_date,
        degree: this.degree,
        university: this.university,
        details: this.details,
      };
      axios
        .post("/api/education", params)
        .then((response) => {
          console.log(response.data);
          this.education.push(response.data);
        })
        .catch((error) => console.log(error.response));
    },
    showEducation: function () {
      document.querySelector("#education-details").showModal();
    },
    updateEducation: function (education) {
      console.log("Updating Eduction info");
      var params = {
        startDate: this.start_date,
        endDate: this.end_date,
        degree: this.degree,
        university: this.university,
        details: this.details,
      };
      axios
        .patch("/api/education" + education.id, params)
        .then((response) => {
          console.log("Success", response.data);
        })
        .catch((error) => console.log(error.response));
    },

    editExperienceModal: function () {
      document.querySelector("#experience-details").showModal();
    },

    createExperience: function () {
      console.log("Creating an experience");
      var params = {
        startDate: this.start_date,
        endDate: this.end_date,
        jobTitle: this.job_title,
        companyName: this.company_name,
        details: this.details,
      };
      axios.post("/api/profile", params).then(() => {
        this.$router.push("/profile");
      });
    },
    createWindow: function () {
      document.querySelector("#create-experience-window").showModal();
    },
    updateExperience: function (experience) {
      var params = {
        startDate: experience.start_date,
        endDate: experience.end_date,
        jobTitle: experience.job_title,
        companyName: experience.company_name,
        details: experience.details,
      };
      axios.patch("/api/experiences/" + experience.id, params).then((response) => {
        console.log("Change Accepted", response.data);
      });
    },
    destroyExperience: function (experience) {
      axios.delete("/api/experiences/" + experience.id).then((response) => {
        console.log("Delete Confirmed", response.data);
        var index = this.experiences.indexOf(experience);
        this.experiences.splice(index, 1);
      });
    },
    targetExperience: function (experience) {
      console.log(experience);
      this.currentExperience = experience;
      document.querySelector("#experience-details").showModal();
    },
    createCapstoneWindow: function () {
      document.querySelector("#create-capstone-window").showModal();
    },
    editCapstoneWindow: function () {
      document.querySelector("#edit-capstone-window").showModal();
    },
  },
};
// };
</script>
