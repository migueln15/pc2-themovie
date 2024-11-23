<template>
  <q-layout view="lHh Lpr lFf">
    <q-page-container>
      <q-page class="flex flex-center q-pa-md" style="height: 100vh">
        <q-card style="max-width: 400px; width: 100%">
          <!-- Encabezado -->
          <q-card-section class="text-center">
            <h5>Inicio de sesión</h5>
            <p class="text-grey-6">Ingresa tus credenciales para continuar</p>
          </q-card-section>

          <!-- Formulario -->
          <q-card-section>
            <q-form @submit.prevent="inicioSesion" ref="loginForm">
              <q-input
                v-model="emailValue"
                filled
                type="email"
                hint="Ingresa tu email"
                label="Correo electrónico"
                required
                :rules="[(val) => !!val || 'El correo es obligatorio']"
              />
              <q-input
                v-model="pwdValue"
                filled
                :type="isPwd ? 'password' : 'text'"
                hint="Ingresa tu contraseña"
                label="Contraseña"
                class="q-mt-md"
                required
                :rules="[(val) => !!val || 'La contraseña es obligatoria']"
              >
                <template v-slot:append>
                  <q-icon
                    :name="isPwd ? 'visibility_off' : 'visibility'"
                    class="cursor-pointer"
                    @click="isPwd = !isPwd"
                  />
                </template>
              </q-input>

              <!-- Botón de inicio de sesión -->
              <q-btn
                label="Iniciar sesión"
                color="primary"
                class="q-mt-lg full-width"
                type="submit"
              />
            </q-form>
          </q-card-section>
        </q-card>
      </q-page>
    </q-page-container>
  </q-layout>
</template>

<style></style>

<script>
export default {
  name: "LoginForm",
  data() {
    return {
      emailValue: "",
      pwdValue: "",
      isPwd: true,
    };
  },
  methods: {
    inicioSesion() {
      console.log("Click en el boton de inici de sesión");
      console.log("Valor del email: " + this.emailValue);

      let endpointLogin = "/api/v1/user/signin ";
      let user = { email: this.emailValue, password: this.pwdValue };

      this.$api
        .post(endpointLogin, user)
        .then((response) => {
          //respuesta exitosa
          //console.log("Respuesta exitosa: " + JSON.stringify(response));
          localStorage.setItem("userData", JSON.stringify(response));
          this.$q.notify({
            message: "Bienvenido a Store APP",
            color: "positive",
            position: "bottom",
            timeout: 5000,
          });

          this.$router.push("/movie");
        })
        .catch((error) => {
          //Ocurrió un error
          this.$q.notify({
            message: "Ocurrió un error",
            color: "negative",
            position: "top",
            timeout: 5000,
          });
          console.log("Error en: " + error);
        });
    },
  },
};
</script>
