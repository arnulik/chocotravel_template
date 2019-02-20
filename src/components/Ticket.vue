<template>
  <div>
    <div class="filter-bar">
      <div class="filter-bar__cell filter-bar__text filter-bar__dropdown">
        Авиакомпании <img src="../assets/filter-bar__down-arrow.png" alt="" />
        <div class="filter-bar__text filter-bar__dropdown-content">
          <div class="filter-bar__checkbox">
            <input
              type="checkbox"
              id="all_airlines"
              @click="selectAll(all_selected);"
              v-model="all_selected"
            />
            <label for="all_airlines"> Все </label>
          </div>
          <div v-for="airline in airlines">
            <div class="filter-bar__checkbox">
              <input
                type="checkbox"
                v-model="airline.is_checked"
                :id="airline.id"
              />
              <label :for="airline.id">{{ airline.title }}</label>
            </div>
          </div>
        </div>
      </div>
      <div class="filter-bar__cell filter-bar__text">
        <label for="straight_airline"> Только прямые рейсы </label>
      </div>
    </div>

    <div class="main-form__grid-header">
      <div class="main-form__grid-header__text">Авиакомпания</div>
      <div class="main-form__grid-header__text">Рейс</div>
      <div class="main-form__grid-header__text">Выбор времени</div>
      <div class="main-form__grid-header__text">Вылет - посадка</div>
      <div class="main-form__grid-header__text">Время в пути</div>
      <div class="main-form__grid-header__text">&nbsp;</div>
    </div>

    <div v-for="data in ticket_json">
      <div v-for="airline in airlines">
        <div
          class="ticket"
          v-show="
            airline.is_checked && data.flights[0].airline.code === airline.code
          "
        >
          <div class="ticket__cell">
            <img
              class="ticket__logo"
              v-if="data.flights[0].airline.code == 'DV'"
              src="../assets/DV.png"
            />
            <img
              class="ticket__logo"
              v-else-if="data.flights[0].airline.code == 'Z9'"
              src="../assets/Z9.png"
            />
            <img
              class="ticket__logo"
              v-else-if="data.flights[0].airline.code == 'KC'"
              src="../assets/KC.png"
            />
          </div>
          <div class="ticket__cell ticket__text">прямой</div>
          <div class="ticket__cell ticket__timing">
            <div>
              Выбрать другое время
              <img src="../assets/ticket__down-arrow.png" alt="" />
            </div>
            <div>Поделиться</div>
          </div>
          <div class="ticket__cell">
            <div class="ticket__departure-time">
              {{ data.flights[0].departureTime }}
            </div>
            <div class="ticket__text">
              &nbsp; {{ "- " + data.flights[0].arrivalTime }}
            </div>
          </div>
          <div class="ticket__cell ticket__text">
            {{ timeConvert(data.flightDuration) }}
          </div>
          <div class="ticket__cell">
            <input
              class="ticket__button"
              type="button"
              v-bind:value="'Купить за ' + data.price + ' kzt'"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import json from "../data/data.json";
export default {
  data() {
    return {
      ticket_json: json,
      all_selected: false,
      airlines: [
        {
          id: 0,
          title: "Air Astana",
          code: "KC",
          is_checked: true
        },
        {
          id: 1,
          title: "Bek Air",
          code: "Z9",
          is_checked: false
        },
        {
          id: 2,
          title: "Scat",
          code: "DV",
          is_checked: true
        }
      ]
    };
  },
  methods: {
    getImagePath(airline_code) {
      return "../assets/" + airline_code + ".png";
    },
    timeConvert(min) {
      var minutes = min % 60;
      var hours = (min - minutes) / 60;
      return hours + "ч " + minutes + "м";
    },
    selectAll: function(all_selected) {
      if (!all_selected) {
        for (let item in this.airlines) {
          this.airlines[item].is_checked = true;
        }
      } else {
        for (let item in this.airlines) {
          this.airlines[item].is_checked = false;
        }
      }
    }
  }
};
</script>

<style lang="scss" src="../styles/body/ticket.scss"></style>
<style lang="scss" src="../styles/body/filter-bar.scss"></style>
