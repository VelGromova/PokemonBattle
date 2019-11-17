<template>
  <environment-component>
    <transition name="fade" mode="out-in">
      <modal-component :action="startGame" :title='modalTitle' v-if="showModal" />
        <section class="battle__container">
          <div class="player">
            <healthbar-component
                :char-name="player.name"
                :char-health="player.health"
                :style="{ width: player.health + '%'}"
            />
            <character-component
                is-player
                :char-is-active="charIsActive"
                :char-name="player.name"
                :animation-name='player.animation'
                @click.native="attack"
                @dblclick.native="specialAttack"
            />
          </div>
          <div class="player">
            <healthbar-component
                :char-name="opponent.name"
                :char-health="opponent.health"
                :style="{ width: opponent.health + '%'}"
            />
            <character-component
                is-opponent
                :char-is-active="charIsActive"
                :charName="opponent.name"
            />
          </div>
      </section>
    </transition>
  </environment-component>
</template>

<script>
import EnvironmentComponent from './EnvironmentComponent';
import ModalComponent from './ModalComponent'
import CharacterComponent from './CharacterComponent';
import HealthbarComponent from './HealthbarComponent';

export default {
  components: {
    EnvironmentComponent,
    ModalComponent,
    CharacterComponent,
    HealthbarComponent
  },
  data() {
    return {
      player: {
        isPlayer: true,
        animation: '',
        name: 'Pikachu',
        health: 100,
      },
      opponent: {
        isOpponent: true,
        animation: '',
        name: 'Charmander',
        health: 100,
      },
      charIsActive: false,
      gameIsRunning: false,
      showModal: false,
      modalTitle: '',
      turns: []
    }
  },
  methods: {
    startGame () {
      this.gameIsRunning = true;
      this.player.health = 100;
      this.opponent.health = 100;
      this.showModal = false;
      this.turns = [];
    },
    changeCharacterState() {
      this.charIsActive = true;
      return setTimeout(() => this.charIsActive = false, 500);
    },
    attack () {
      this.changeCharacterState();
      var damage = this.calculateDamage(3, 10);
      this.opponent.health -= damage;
      this.turns.unshift({
        isPlayer: true,
      });
      if (this.checkWin()) {
        return;
      }
      this.opponentAttacks();
    },
    specialAttack () {
      this.changeCharacterState;
      var damage = this.calculateDamage(10, 20);
      this.opponent.health -= damage;
      this.turns.unshift({
        isPlayer: true,
      });
      if (this.checkWin()) {
        return;
      }
      this.opponentAttacks();
    },
    opponentAttacks() {
      var damage = this.calculateDamage(5, 12);
      this.player.health -= damage;
      this.checkWin();
      this.turns.unshift({
        isPlayer: false,
      });
    },
    calculateDamage(min, max) {
      return Math.max(Math.floor(Math.random() * max) + 1, min);
    },
    checkWin() {
        if (this.opponent.health <= 0) {
          this.modalTitle = 'Congrats! You won!';
            this.showModal = true;
          return true;
        } else if (this.player.health <= 0) {
          this.modalTitle = 'Oops...You lost!';
            this.showModal = true;
          return true;
        }
        return false;
      },
  }
}
</script>

<style lang="scss">
  .battle__container {
    display: flex;
    flex-wrap: nowrap;
    justify-content: space-around;
    .player {
      height: 90vh;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
    }
}

</style>
