<template>
  <div id="dialog_app">
    <transition name="modal">
      <div class="modal-mask">
        <div class="modal-wrapper">
          <div class="modal-container">
            <div class="modal-header">
              <slot name="header"> Выберете параметры функции </slot>
            </div>

            <div class="modal-body">
              <slot name="body">
                <form class="form-floating">
                  <input
                    type="text"
                    class="form-control"
                    id="floatingInputValue"
                    v-model="A"
                    autocomplete="off"
                  />
                  <label for="floatingInputValue">Param A</label>
                </form>

                <form class="form-floating">
                  <input
                    type="text"
                    class="form-control"
                    id="floatingInputValue"
                    v-model="B"
                    autocomplete="off"
                  />
                  <label for="floatingInputValue">Param B</label>
                </form>
                <form class="form-floating">
                  <input
                    type="text"
                    class="form-control"
                    id="floatingInputValue"
                    v-model="C"
                    autocomplete="off"
                  />
                  <label for="floatingInputValue">Param C</label>
                </form>
              </slot>
            </div>

            <div class="modal-footer">
              <slot name="footer">
                <button
                  class="modal-default-button btn btn-secondary"
                  @click="closeDialog"
                >
                  Закрыть {{test}}
                </button>
                <button
                  class="modal-default-button btn btn-primary"
                  @click="saveParametrs"
                >
                  Сохранить
                </button>
              </slot>
            </div>
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  name: "dialog_app",
  data() {
    return {
      A: this.Aprop,
      B: this.Bprop,
      C: this.Cprop,
    };
  },
  props: ['Aprop', 'Bprop', 'Cprop'],
  methods: {
    saveParametrs() {
      this.$emit("updateData", {
        aParam: this.A,
        bParam: this.B,
        cParam: this.C,
      });
    },
    closeDialog() {
      this.$emit("closeDialog");
    },
  },
};
</script>

<style>
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  width: 300px;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
  font-family: Helvetica, Arial, sans-serif;
}
.modal-header h3 {
  margin-top: 0;
  color: #42b983;
}

.modal-body {
  margin: 20px 0;
  padding: 10px 10px;
}

.modal-default-button {
  float: right;
}

/*
   * The following styles are auto-applied to elements with
   * transition="modal" when their visibility is toggled
   * by Vue.js.
   *
   * You can easily play with the modal transition by editing
   * these styles.
   */

.modal-enter {
  opacity: 0;
}

.modal-leave-active {
  opacity: 0;
}

.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
li {
  list-style-type: none; /* Убираем маркеры */
}
ul {
  margin-left: 0; /* Отступ слева в браузере IE и Opera */
  padding-left: 0; /* Отступ слева в браузере Firefox, Safari, Chrome */
}
.close {
  background-color: green;
}
.form-floating {
  margin-bottom: 12px;
}
</style>