<template>
  <div class="main">
    <h1 class="main__headline headline">Специализированные дисциплины</h1>
    <ul class="courses-list list">
      <li class="courses-list__item" v-for="course in courses" :key="course.id">
        <h3 class="courses-list__title">{{ course.title }}</h3>
        <button
          :id="course.title"
          type="button"
          @click="activateButton"
          class="courses-list__module first_module"
        >
          1 модуль
        </button>
        <button
          :id="course.title"
          type="button"
          @click="activateButton"
          class="courses-list__module seckond_module"
        >
          2 модуль
        </button>
        <ul class="subjects-list list" :id="course.title">
          <li
            class="subjects-list__item none"
            v-for="subject in course.specializedSubjects"
            :key="subject.id"
          >
            <p class="subjects-list__text">{{ subject }}</p>
          </li>
        </ul>
      </li>
    </ul>
    <ul class="modules-list list">
      <li class="modules-list__item" v-for="module in modules" :key="module.id">
        <h1 class="modules-list__headline headline">{{ module.headline }}</h1>
        <ul class="descriptions-list list">
          <li
            class="descriptions-list__item"
            v-for="description in module.descriptions"
            :key="description.id"
            :class="{ description_dot: module.dot }"
          >
            <p class="modules-list__description">{{ description }}</p>
          </li>
        </ul>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",

  data() {
    return {
      courses: null,
      modules: [
        {
          headline: "Практические модули",
          descriptions: [
            "Работа над собственными проектами: практика групповых взаимодействий, кейс-методы, эссе",
          ],
        },
        {
          dot: true,
          headline: "Итоговая аттестация",
          descriptions: [
            "Бизнес-проектирование (подготовка итоговой аттестационной работы, консультирование по бизнес-проектированию)",
            "Защита итоговой аттестационной работы",
          ],
        },
      ],
    };
  },

  mounted() {
    axios
      .get(
        "https://ipo-cp.ru/api/v1/bootcamps/605c5f71bc557b46b4f42a56/courses"
      )
      .then((response) => (this.courses = response.data.data));
  },

  methods: {
    activateButton: function (event) {
      event.target.classList.toggle("activeModule");
      let subjectsLists = document.querySelectorAll(".subjects-list");
      subjectsLists.forEach((subjectsList) => {
        if (
          subjectsList.id === event.target.id &&
          event.target.classList.contains("first_module")
        ) {
          subjectsList.classList.toggle("start5");
        }
        if (
          subjectsList.id === event.target.id &&
          event.target.classList.contains("seckond_module")
        ) {
          subjectsList.classList.toggle("end5");
        }
      });
    },
  },
};
</script>
