<template>
  <v-dialog :value="value" width="750" @input="$emit('input', false)">
    <v-card>
      <v-card-title>
        <h3>
          Are you sure you want to delete
          <span class="carrier">{{ roleTitle }}</span>
          ?
        </h3>
      </v-card-title>
      <v-card-actions class="d-flex justify-end">
        <v-btn color="primary" text @click="$emit('input', false)">
          Cancel
        </v-btn>
        <v-btn color="error" @click="onDeleteRole">
          Delete
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>
<script>
import { mapActions } from "vuex";
export default {
  name: "DeleteRoleConfirmation",
  props: {
    value: {
      type: Boolean,
      default: false,
    },
    roleId: {
      type: Number,
      required: true,
    },
    roleTitle: {
      type: String,
      required: true,
    },
  },
  methods: {
    ...mapActions("roles", ["deleteRole"]),
    ...mapActions("alerts", ["displaySuccess"]),
    onDeleteRole: function() {
      this.deleteRole(this.roleId);
      this.$emit("input", false);
      this.displaySuccess("Role deleted");
      this.$router.push("/roles");
    },
  },
};
</script>
<style lang="scss" scoped>
.carrier {
  background-color: rgba(200, 200, 200, 0.5);
  border-radius: 6px;
  padding: 0.25rem;
}
</style>
