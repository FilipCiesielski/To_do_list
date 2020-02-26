<template>
  <div class="to_do__box__container">
    <img class="tapeLeft" src="../assets/tape.png" />
    <div class="to_do__box1"></div>
    <div class="to_do__box">
      <div><h1>to do list...</h1></div>
      <div class="to_do__box__elements">
        <ul>
          <li
            v-for="(toDo, index) in toDoList"
            :key="toDo.task + index"
            :class="{ active: toDo.isDone }"
          >
            <template v-if="toDo.task.length > 0"
              ><p>{{ toDo.task }}</p>
              <!-- <input type="checkbox" v-model="toDo.isDone" /> -->
              <input
                type="checkbox"
                class="form-checkbox"
                checked=""
                v-model="toDo.isDone"
              />
              <button @click="removeItemSubmit(toDo.id)" id="removeNewTodo">
                <svg
                  aria-hidden="true"
                  focusable="false"
                  data-prefix="far"
                  data-icon="trash-alt"
                  class="svg-inline--fa fa-trash-alt fa-w-14"
                  role="img"
                  xmlns="http://www.w3.org/2000/svg"
                  viewBox="0 0 448 512"
                >
                  <path
                    fill="currentColor"
                    d="M268 416h24a12 12 0 0 0 12-12V188a12 12 0 0 0-12-12h-24a12 12 0 0 0-12 12v216a12 12 0 0 0 12 12zM432 80h-82.41l-34-56.7A48 48 0 0 0 274.41 0H173.59a48 48 0 0 0-41.16 23.3L98.41 80H16A16 16 0 0 0 0 96v16a16 16 0 0 0 16 16h16v336a48 48 0 0 0 48 48h288a48 48 0 0 0 48-48V128h16a16 16 0 0 0 16-16V96a16 16 0 0 0-16-16zM171.84 50.91A6 6 0 0 1 177 48h94a6 6 0 0 1 5.15 2.91L293.61 80H154.39zM368 464H80V128h288zm-212-48h24a12 12 0 0 0 12-12V188a12 12 0 0 0-12-12h-24a12 12 0 0 0-12 12v216a12 12 0 0 0 12 12z"
                  ></path>
                </svg>
              </button>
            </template>
            <template v-else>
              <input
                type="text"
                placeholder=">write here<"
                @keyup.enter="onNewItemSubmit(toDo)"
                v-model="toDo.temporaryTask"
              />
              <button @click="onNewItemSubmit(toDo)" id="addNewTodo">
                <svg
                  aria-hidden="true"
                  focusable="false"
                  data-prefix="fas"
                  data-icon="pencil-alt"
                  class="svg-inline--fa fa-pencil-alt fa-w-16"
                  role="img"
                  xmlns="http://www.w3.org/2000/svg"
                  viewBox="0 0 512 512"
                >
                  <path
                    fill="currentColor"
                    d="M497.9 142.1l-46.1 46.1c-4.7 4.7-12.3 4.7-17 0l-111-111c-4.7-4.7-4.7-12.3 0-17l46.1-46.1c18.7-18.7 49.1-18.7 67.9 0l60.1 60.1c18.8 18.7 18.8 49.1 0 67.9zM284.2 99.8L21.6 362.4.4 483.9c-2.9 16.4 11.4 30.6 27.8 27.8l121.5-21.3 262.6-262.6c4.7-4.7 4.7-12.3 0-17l-111-111c-4.8-4.7-12.4-4.7-17.1 0zM124.1 339.9c-5.5-5.5-5.5-14.3 0-19.8l154-154c5.5-5.5 14.3-5.5 19.8 0s5.5 14.3 0 19.8l-154 154c-5.5 5.5-14.3 5.5-19.8 0zM88 424h48v36.3l-64.5 11.3-31.1-31.1L51.7 376H88v48z"
                  ></path>
                </svg>
              </button>
            </template>
          </li>
          <li
            v-for="toDo in doneList"
            :key="toDo.task"
            :class="{ active: toDo.isDone }"
          >
            <p>{{ toDo.task }}</p>
            <input
              type="checkbox"
              class="form-checkbox"
              checked=""
              v-model="toDo.isDone"
            />
          </li>
        </ul>
      </div>
      <button id="onButtonClick" @click="onNewItemButtonClick">add new</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "To_do_list",
  data() {
    return {
      listData: []
    };
  },
  computed: {
    toDoList: function() {
      return this.listData.filter(el => {
        return el.isDone == false;
      });
    },
    doneList: function() {
      return this.listData.filter(el => {
        return el.isDone == true;
      });
    }
  },
  methods: {
    onNewItemButtonClick: function() {
      let newTaskToDo = {
        id: Date.now(),
        task: "",
        isDone: false
      };
      this.listData.unshift(newTaskToDo);
    },
    onNewItemSubmit: function(item) {
      item.task = item.temporaryTask;
      delete item.temporaryTask;
    },
    removeItemSubmit: function(id) {
      let currentId = id;
      console.log(currentId);
      this.listData = this.listData.filter(function(val) {
        return val.id !== currentId;
      });
    }
  }
};
</script>

<style lang="scss">
.to_do__box__container {
  position: relative;
  width: 100%;
  padding: 1rem;
  .tapeLeft {
    position: absolute;
    width: 12rem;
    transform: translateX(-50%) rotate(-48deg);
    z-index: 2;
    left: 50%;
    top: -85px;
  }
  .to_do__box {
    display: flex;
    align-items: center;
    flex-direction: column;
    width: 100%;
    background-color: #fff740;
    -webkit-box-shadow: 5px 15px 0px 2px rgba(254, 255, 156, 1);
    -moz-box-shadow: 5px 15px 0px 2px rgba(254, 255, 156, 1);
    box-shadow: 5px 15px 0px 2px rgba(254, 255, 156, 1);
    position: relative;
    &::before {
      content: "";
      display: flex;
      align-items: center;
      flex-direction: column;
      width: 100%;
      height: 100%;
      background-color: #7afcff;
      -webkit-box-shadow: -2px 7px 28px -6px rgba(0, 0, 0, 0.75);
      -moz-box-shadow: -2px 7px 28px -6px rgba(0, 0, 0, 0.75);
      box-shadow: -2px 7px 28px -6px rgba(0, 0, 0, 0.75);
      transform: rotate(-2deg);
      overflow: hidden;
      position: absolute;
      z-index: -1;
      top: 7%;
    }
    &::after {
      content: "";
      display: flex;
      align-items: center;
      flex-direction: column;
      width: 100%;
      height: 100%;
      background-color: #ff65a3;
      -webkit-box-shadow: 5px 12px 0px 2px rgb(255, 126, 185);
      -moz-box-shadow: 5px 12px 0px 2px rgba(255, 126, 185, 1);
      box-shadow: 5px 12px 0px 2px rgba(255, 126, 185, 1);
      overflow: hidden;
      position: absolute;
      z-index: -2;
      top: 10%;
      transform: rotate(-4deg);
    }
    h1 {
      display: flex;
      color: #44b9bbf3;
      align-items: center;
      justify-content: flex-start;
      padding-top: 1rem;
      margin-top: 2rem;
      margin-right: 5rem;
      transform: rotate(-12deg);
    }
    .to_do__box__elements {
      padding-bottom: 20px;
      width: 100%;
      &::-webkit-scrollbar {
        display: none; /* Safari and Chrome */
      }
      display: flex;
      align-items: center;
      margin-top: 1rem;
      min-height: 16rem;
      max-height: 20px;
      flex-direction: column;
      overflow-y: scroll;
      ul {
        width: 90%;
        input[type="text"] {
          width: 60%;
          font-size: 1.6rem;
          background: none;
          border: none;
          font-family: "Indie Flower";
        }
        .form-checkbox:checked {
          background-image: url(../assets/check.svg);
          color: #44b9bbf3;
          border-color: transparent;
          background-color: transparent;
          background-size: 100% 100%;
          background-position: center;
          background-repeat: no-repeat;
        }
        .form-checkbox {
          margin-left: auto;
          -webkit-appearance: none;
          -moz-appearance: none;
          appearance: none;
          -webkit-print-color-adjust: exact;
          color-adjust: exact;
          display: inline-block;
          vertical-align: middle;
          background-image: url(../assets/check.svg);
          background-origin: border-box;
          -webkit-user-select: none;
          -moz-user-select: none;
          -ms-user-select: none;
          user-select: none;
          flex-shrink: 0;
          height: 1.8rem;
          width: 1.8rem;
          color: #44b9bbf3;
          border-width: 1px;
          border-radius: 50px;
        }
        ::placeholder {
          font-size: 1.6rem;
        }
        li {
          display: flex;
          align-items: center;
          justify-content: space-between;
          margin-top: 1rem;
          list-style-type: none;
          border-radius: 5px;
          border: 1px solid grey;
          color: grey;
          padding: 0.6rem 1rem 0.6rem 1rem;
          font-size: 1.7rem;

          &.active {
            background-color: #ff7eb9;
            text-decoration: line-through;
          }
        }
      }
      #addNewTodo,
      #removeNewTodo {
        width: 2.5rem;
        height: 2.5rem;
        padding: 0.5rem;
        background: transparent;
        border: none;
        color: #44b9bbf3;
        cursor: pointer;
      }
    }
    #onButtonClick {
      width: 4rem;
      height: 4rem;
      padding: 1rem;
      border-radius: 50%;
      color: grey;
      font-weight: bold;
      top: 2rem;
      right: 10%;
      position: absolute;
      z-index: 20;
      cursor: pointer;
    }
  }
}
</style>
