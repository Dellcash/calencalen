<!-- <template>
    <div style="margin: 1rem">
        <div
            id="g_id_onload"
            :data-client_id="googleClientId"
            data-callback="handleCredentialResponse"
        ></div>
        <div
            class="g_id_signin"
            data-type="standard"
        ></div>

        <button @click="loadCalendarEvents">Load Calendar Events</button>
        <ul v-if="calendarEvents.length">
            <li
                v-for="event in calendarEvents"
                :key="event.id"
            >
                {{ event.summary }}
            </li>
        </ul>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { OAuth2Client } from 'google-auth-library';

const googleClientId = '519386071351-rqcv4i0ojgbk8son24m2d0ldoflscc1i.apps.googleusercontent.com'; // Replace with your actual Client ID
const calendarEvents = ref([]);
const identityService = new OAuth2Client();

const loadCalendarEvents = async () => {
    try {
        await identityService.signIn();
        if (identityService.isSignedIn()) {
            // Initialize the Google Calendar API client
            gapi.load('client', () => {
                gapi.client.init({
                    apiKey: 'AIzaSyDQoJeTSX4-L8fNsto4FjBDy4rA0Di7GOQ',
                    clientId: googleClientId,
                    discoveryDocs: ['https://www.googleapis.com/discovery/v1/apis/calendar/v3/rest'],
                    scope: 'https://www.googleapis.com/auth/calendar.readonly',
                }).then(() => {
                    // Google Calendar API client is initialized, fetch events
                    gapi.client.calendar.events
                        .list({
                            calendarId: 'primary',
                            timeMin: new Date().toISOString(),
                            showDeleted: false,
                            singleEvents: true,
                            maxResults: 10,
                            orderBy: 'startTime',
                        })
                        .then((response) => {
                            calendarEvents.value = response.result.items;
                        })
                        .catch((error) => {
                            console.error('Error loading calendar events: ', error);
                        });
                });
            });
        }
    } catch (error) {
        console.error('Google Sign-In Error: ', error);
    }
};

onMounted(() => {
    identityService.loadGoogleIdentityService({
        client_id: googleClientId,
    });
});
</script> -->

<template>
    <div style="margin: 1rem">
        <div
            id="g_id_onload"
            :data-client_id="googleClientId"
            data-callback="handleCredentialResponse"
        ></div>
        <div
            class="g_id_signin"
            data-type="standard"
        ></div>

        <button @click="loadCalendarEvents">Load Calendar Events</button>
        <ul v-if="calendarEvents.length">
            <li
                v-for="event in calendarEvents"
                :key="event.id"
            >
                {{ event.summary }}
            </li>
        </ul>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const googleClientId = '519386071351-rqcv4i0ojgbk8son24m2d0ldoflscc1i.apps.googleusercontent.com';
const calendarEvents = ref([]);
const isScriptLoaded = ref(false);

const loadExternalScript = () => {
    // Load the external script from the CDN
    const script = document.createElement('script');
    script.src = 'https://accounts.google.com/gsi/client';
    script.async = true;
    script.onload = () => {
        // Script has been loaded
        isScriptLoaded.value = true;
    };

    // Append the script to the document
    document.head.appendChild(script);
};

const loadCalendarEvents = () => {
    // Ensure the Google API script is loaded before initializing
    if (!window.gapi) {
        console.error('Google API Client Library is not loaded.');
        return;
    }

    // Initialize the Google Calendar API client
    gapi.load('client', () => {
        gapi.client.init({
            apiKey: 'AIzaSyDQoJeTSX4-L8fNsto4FjBDy4rA0Di7GOQ',
            clientId: googleClientId,
            discoveryDocs: ['https://www.googleapis.com/discovery/v1/apis/calendar/v3/rest'],
            scope: 'https://www.googleapis.com/auth/calendar.readonly',
        }).then(() => {
            // Google Calendar API client is initialized, fetch events
            gapi.client.calendar.events
                .list({
                    calendarId: 'primary', // Use 'primary' for the user's primary calendar
                    timeMin: new Date().toISOString(),
                    showDeleted: false,
                    singleEvents: true,
                    maxResults: 10, // Adjust as needed
                    orderBy: 'startTime',
                })
                .then((response) => {
                    calendarEvents.value = response.result.items;
                })
                .catch((error) => {
                    console.error('Error loading calendar events: ', error);
                });
        });
    });
};

loadExternalScript(); 
</script>

<!-- <template>
    <div style="margin: 1rem">
        <div
            id="g_id_onload"
            data-client_id="519386071351-rqcv4i0ojgbk8son24m2d0ldoflscc1i.apps.googleusercontent.com"
            data-callback="handleCredentialResponse"
        ></div>
        <div
            class="g_id_signin"
            data-type="standard"
        ></div>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const isScriptLoaded = ref(false)
const loadExternalScript = () => {
    // Load the external script from the CDN
    const script = document.createElement('script');
    script.src = 'https://accounts.google.com/gsi/client';
    script.async = true;
    script.onload = () => {
        // Script has been loaded
        isScriptLoaded.value = true;
    };

    console.log('script', script);
    // Append the script to the document
    document.head.appendChild(script);
}

loadExternalScript()
</script> -->


<!-- < template >
    <div>
        <div
            id="g_id_onload"
            :data-client_id="clientId"
            data-callback="handleCredentialResponse"
        ></div>
        <div
            class="g_id_signin"
            data-type="standard"
        ></div>
    </div >
</template > -->

<!-- <template>
    <div
        id="g_id_onload"
        data-client_id="519386071351-rqcv4i0ojgbk8son24m2d0ldoflscc1i.apps.googleusercontent.com"
        data-callback="handleCredentialResponse"
    >
    </div>
    <div
        class="g_id_signin"
        data-type="standard"
    ></div>
    <div>
        <button @click="signInWithGoogle">Sign In with Google</button>
        <div v-if="isSignedIn">
            <p>Welcome, {{ userName }}!</p>
            <button @click="signOut">Sign Out</button>
        </div>
    </div>
</template> -->

<!-- <script setup>
import { ref, onMounted } from 'vue';

const isSignedIn = ref(false);
const userName = ref('');

const initGoogleApi = async () => {
    try {
        await new Promise((resolve) => {
            gapi.load('client:auth2', resolve);
        });

        const auth2 = await gapi.auth2.init({
            client_id: '519386071351-rqcv4i0ojgbk8son24m2d0ldoflscc1i.apps.googleusercontent.com', // Replace with your new Client ID
        });

        // Now, auth2 is initialized, and you can use it for sign-in
        return auth2;
    } catch (error) {
        console.error('Google API Initialization Error: ', error);
    }
};

const signInWithGoogle = async () => {
    try {
        const auth2 = await initGoogleApi();

        // Ensure that the Google API Client Library is initialized
        // if (!auth2) {
        //     console.error('Google API Client Library is not initialized.');
        //     return;
        // }

        console.log('auth', auth2);
        const auth2 = auth2.getAuthInstance();
        const user = await auth2.signIn();
        isSignedIn.value = true;
        userName.value = user.getBasicProfile().getName();
    } catch (error) {
        console.error('Google Sign-In Error: ', error);
    }
};

onMounted(() => {
    signInWithGoogle();
});
</script> -->



<!-- <script setup>
import { ref, onMounted } from 'vue';

const isSignedIn = ref(false);
const userName = ref('');

const initGoogleApi = async () => {
    try {
        await new Promise((resolve) => {
            gapi.load('client:auth2', resolve);
        });

        const auth2 = await gapi.auth2.init({
            // client_id: '470300798985-ao1tkcsr81gpnh55hcjifg1qoc0a7245.apps.googleusercontent.com'
            client_id: '519386071351-rqcv4i0ojgbk8son24m2d0ldoflscc1i.apps.googleusercontent.com',
        });

        // Now, auth2 is initialized, and you can use it for sign-in
        return auth2
    } catch (error) {
        console.error('Google API Initialization Error: ', error);
    }
};

const signInWithGoogle = async () => {
    try {
        // Ensure that the Google API Client Library is initialized
        if (!gapi.auth2.getAuthInstance()) {
            console.error('Google API Client Library is not initialized.');
            return;
        }

        const auth2 = gapi.auth2.getAuthInstance();
        const user = await auth2.signIn();
        isSignedIn.value = true;
        userName.value = user.getBasicProfile().getName();
    } catch (error) {
        console.error('Google Sign-In Error: ', error);
    }
};

const signOut = async () => {
    try {
        await gapi.load('auth2', async () => {
            const auth2 = await gapi.auth2.getAuthInstance();
            await auth2.signOut();
            isSignedIn.value = false;
            userName.value = '';
        });
    } catch (error) {
        console.error('Google Sign-Out Error: ', error);
    }
};

onMounted(() => {
    initGoogleApi()
});
</script> -->
