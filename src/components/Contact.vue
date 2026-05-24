<script setup>
    import { ref, onMounted, onUnmounted } from 'vue';

    import { Notyf } from 'notyf';
    import 'notyf/notyf.min.css';

    const notyf = new Notyf();

    const WEB3FORMS_ACCESS_KEY = "cf5118e6-3cbb-4f5a-bc25-65ff6aeec143";

    const subject = "New message from Portfolio Contact Form";

    const name = ref("");
    const email = ref("");
    const message = ref("");

    const isLoading = ref(false);


    const submitForm = async() => {

        if(!recaptchaToken.value) {
            notyf.error('Please verify that you are not a robot.');
            return;
        }

        isLoading.value = true;

        try {

            const response = await fetch("https://api.web3forms.com/submit", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                    Accept: "application/json"
                },
                body: JSON.stringify({
                    access_key: WEB3FORMS_ACCESS_KEY,
                    subject: subject,
                    name: name.value,
                    email: email.value,
                    message: message.value
                })
            });

            const result = await response.json();

            if(result.success) {
                console.log(result)

                isLoading.value = false;
                notyf.success("Message sent!");
            }

        } catch(error) {
            console.log(error);

            isLoading.value = false;
            notyf.error("Failed to send message");

        } finally {

            resetRecaptcha();
        }
    }

    /*recaptcha integration*/

    const SITE_KEY = '6LehxvksAAAAAJ1R7SYgEaPe8HrhMYNd14-EcCv4';

    const recaptchaContainer = ref(null);
    const recaptchaWidgetId = ref(null);
    const recaptchaToken = ref('');


    function onRecaptchaSuccess(token) {
        recaptchaToken.value = token;
    }

    function onRecaptchaExpired() {
        recaptchaToken.value = '';
    }

    function renderRecaptcha() {
        if(!window.grecaptcha) {
            console.error('reCAPTCHA not loaded');
            return;
        }

        recaptchaWidgetId.value = window.grecaptcha.render(recaptchaContainer.value, {
            sitekey: SITE_KEY,
            size: 'normal',
            callback: onRecaptchaSuccess,
            'expired-callback': onRecaptchaExpired
        });
    }

    function resetRecaptcha() {
        if(recaptchaWidgetId.value !== null) {
            window.grecaptcha.reset(recaptchaWidgetId.value);
            recaptchaToken.value = '';
        }
    }

    onMounted(() => {
        const interval = setInterval(() => {
            if(window.grecaptcha && window.grecaptcha.render) {
                renderRecaptcha();
                clearInterval(interval)
            }
        }, 100);

        onBeforeMount(() => {
            clearInterval(interval);
        });
    })

</script>

<template>
                <!-- contact -->
                <h1 class="text-center my-4 pt-5" id="contact">Contact</h1>
                <div class="contact-section">
                    <div class="row align-items-center mt-4">
                        <div class="col-md-6 map-container">
                            <iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d2529.422282537867!2d120.35089902756451!3d16.07136882908666!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x33916998f3385671%3A0x9fd7fc41e2246132!2sGrandiaGo%20Pangasinan!5e0!3m2!1sen!2sph!4v1775687530107!5m2!1sen!2sph"
                        allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade">
                        </iframe>
                        </div>
                        <div class="col-md-6">
                            <form @submit.prevent="submitForm">
                                <div class="mb-3">
                                    <input type="text"
                                     v-model="name"
                                     class="form-control contact-form-control" placeholder="First Name M.I. Last Name">
                                </div>
                                <div class="mb-3">
                                    <input type="email"
                                    v-model="email"
                                    class="form-control contact-form-control" placeholder="Email">
                                </div>
                                <div class="mb-3">
                                    <textarea 
                                    v-model="message"
                                    class="form-control contact-form-control" rows="6" placeholder="Message"></textarea>
                                </div>
                                <div class="form-footer">
                                    <div class="social-icons">
    <!--                                <a href="https://www.facebook.com/profile.php?id=100085701498879" id="facebook"><i class="fab fa-facebook"></i></a> -->
                                        <a href="https://www.linkedin.com/in/charles-babbage-8291a6211/" id="linkedin"><i class="fab fa-linkedin"></i></a>
                                        <a href="https://gitlab.com/cbabbage0991" id="gitlab"><i class="fab fa-gitlab"></i></a>
                                        <a href="https://github.com/cbabbage0991" id="github"><i class="fab fa-github"></i></a>
                                    </div>
                                    <button type="submit" class="submit-btn pl-5 pr-5" :disabled="isLoading">{{isLoading ? "Sending..." : "Submit"}}</button>
                                </div>

                                <div class="d-flex justify-content-end mt-2">
                                    <div ref="recaptchaContainer"></div>
                                </div>
                            </form>
                            
                        </div>
                    </div>
                </div>
</template>
