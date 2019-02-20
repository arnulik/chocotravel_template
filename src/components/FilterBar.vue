<template>
  <div>
    <div class="filter-bar">
      <div class="filter-bar__cell filter-bar__text filter-bar__dropdown">
        Авиакомпании
        <div class="filter-bar__text filter-bar__dropdown-content">
          <div v-for="airline in airlines">
            <div class="filter-bar__checkbox">
              <input
                type="checkbox"
                v-model="airline.is_checked"
                :id="airline.id"
              />
              <label :for="airline.id">{{
                airline.title + " " + airline.is_checked
              }}</label>
            </div>
          </div>
        </div>
      </div>
      <div class="filter-bar__cell filter-bar__text">
        <label for="straight_airline"> Только прямые рейсы </label>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      airlines: [
        {
          id: 0,
          title: "Air Astana",
          is_checked: true
        },
        {
          id: 1,
          title: "Bek Air",
          is_checked: false
        },
        {
          id: 2,
          title: "Scat",
          is_checked: true
        }
      ]
    };
  },
  methods: {}
};
</script>

<style lang="scss" src="../styles/body/filter-bar.scss"></style>
