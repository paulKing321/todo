<template>
  <div class="toast-wrapper">
      <div class="toast">
          Oga enter a value for the todo!!
      </div>
  </div>
</template>

<script>
export default {

}
</script>

<style>
.toast-wrapper {
    position: fixed;
    width: 100%;
    top: 20px;
}
.toast {
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 20px;
    color: white;
    background: #ff0062;
    border-radius: 10px;
    box-shadow: 1px 3px 5px rgba(0,0,0,0.2);
    max-width: 400px;
    margin-top: 70px;
    margin-left: 320px;
}

.toast-enter-active {
    animation: wobble 0.5s ease;
}
.toast-leave-to {
    opacity: 0;
    transform: translateY(-60px);
}
.toast-leave-active {
    transition: all 0.3s ease;
}

@keyframes wobble {
    0% { transform: translateY(-100px); opacity: 0;}
    50% { transform: translateY(0px); opacity: 1;}
    60% { transform: translateY(8px); opacity: 1;}
    70% { transform: translateY(-8px); opacity: 1;}
    80% { transform: translateY(-4px); opacity: 1;}
    90% { transform: translateY(-4px); opacity: 1;}
    100% { transform: translateY(0px); opacity: 1;}
}

@media screen and (max-width: 770px) {
    .toast-wrapper, .toast {
    display: flex;
    size: 5px;
    flex-direction: column;
    align-items: centre;
    justify-content: center;
    width: 80%;
    margin: auto;
    padding: 5px;
    margin-top: 30px;
    margin-left: -8px;
    }
}
</style>