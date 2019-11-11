<template>
  <el-row :gutter="20" class="formRow">
    <el-col :span="1">
      <span class="vline seq">{{ value.id }}</span>
    </el-col>
    <el-col :span="5">
      <el-input placeholder="Name" v-model="name"></el-input>
      <div class="validation" v-show="!validation.name.valid">Name is not valid</div>
    </el-col>
    <el-col :span="6">
      <el-input placeholder="Email" v-model="email"></el-input>
      <div class="validation" v-show="!validation.email.valid">Email is not valid</div>
    </el-col>
    <el-col :span="12">
      <el-checkbox-group v-model="juices" class="vline left">
        <el-checkbox label="Apple Juice"></el-checkbox>
        <el-checkbox label="Orange Juice"></el-checkbox>
        <el-checkbox label="Watermelon Juice"></el-checkbox>
      </el-checkbox-group>
      <div class="validation" v-show="!validation.juices.valid">Juices is not valid</div>
    </el-col>
  </el-row>
</template>

<script>
export default {
  name: 'customer-form',
  props: {
    id: Number,
    value: {
      type: Object,
      default() {
        return {
          id: '',
          name: '',
          email: '',
          juices: [],
        };
      },
    },
    validation: {
      type: Object,
      default() {
        return {
          name: { valid: true },
          email: { valid: true },
          juices: { valid: true }
        }
      }
    }
  },
  data() {
    return {
      name: this.value.name,
      email: this.value.email,
      juices: [...this.value.juices],
    };
  },
  watch: {
    name() {
      const c = { id: this.value.id, name: this.name, email: this.email, juices: [...this.juices] };
      this.$emit('input', c);
    },
    email() {
      const c = { id: this.value.id, name: this.name, email: this.email, juices: [...this.juices] };
      this.$emit('input', c);
    },
    juices() {
      const c = { id: this.value.id, name: this.name, email: this.email, juices: [...this.juices] };
      this.$emit('input', c);
    },
    value(newValue, oldValue) {
      const { name, email, juices } = newValue;
      if (name !== oldValue.name) {
        this.name = name;
      }
      if (email !== oldValue.email) {
        this.email = email;
      }
      if (!juices.every( e => oldValue.juices.includes(e)) ) {
        this.juices = [...juices];
      }
    }
  },
}
</script>

<style scoped>
.formRow {
  padding: 12px;
}
.vline {
  line-height: 40px;
}
.left {
  text-align: left;
}
.seq {
  text-align: right;
}
.validation {
  position: absolute;
  margin-top: 2px;
  line-height: 1;
  color: red;
}
</style>