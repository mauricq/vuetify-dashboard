<template>
    <v-container>
        <v-row>
            <v-col>
                <h1>Signup</h1>
                <v-form ref="signUpForm" v-model="formValidity">
                    <v-text-field type="email" label="Email" v-model="email" :rules="emailRules" required></v-text-field>
                    <v-autocomplete
                        label="Wich browser do you use?"
                        :items="browser"
                    ></v-autocomplete>
                    <v-file-input multiple label="Attach profile picture"></v-file-input>
                    <v-text-field label="Birthday" v-model="birthday" readonly></v-text-field>
                    <v-date-picker v-model="birthday"></v-date-picker>
                    <v-checkbox label="Agree to terms & conditions" :rules="agreeToTermsRules" required></v-checkbox>
                    <v-btn class="mr-1" type="submit" color="primary" :disabled="!formValidity">Submit</v-btn>
                    <v-btn class="mr-1" color="success" @click="validateForm">Validate Form</v-btn>
                    <v-btn class="mr-1" color="warning" @click="resetValidation">Reset Validation</v-btn>
                    <v-btn color="error" @click="resetForm">Reset</v-btn>
                </v-form>
            </v-col>
        </v-row>
        
    </v-container>
</template>

<script>
    export default {
     data() {
         return {
             formValidity: false,
             agreeToTerms: false,
             agreeToTermsRules: [
                 value => !!value || 'You must agree to the terms and conditions to sign up for an account.'
             ],
             email: '',
             emailRules: [
                value => value.indexOf('@') !== 0 || 'Email should have a username.',
                value => value.includes('@') || 'Email should include an @ symbol.',
                value =>
                value.indexOf('.') - value.indexOf('@') > 1 ||
                'Email should contain a valid domain.',
                value => value.includes('.') || 'Email should include a period symbol.',
                value =>
                value.indexOf('.') <= value.length - 3 ||
                'Email should contain a valid domain extension.'
             ],
             birthday: new Date().toISOString().substr(0, 10),
             browser: ['Chrome', 'Safari', 'Firefox', 'Edge', 'Brave']
         }
     },
     methods: {
        resetForm() {
            this.$refs.signUpForm.reset()
        },
        resetValidation() {
            this.$refs.signUpForm.resetValidation()
        },
        validateForm() {
            this.$refs.signUpForm.validate()
        }
     },
    }
</script>

<style lang="scss" scoped>

</style>