<template>
  <div class="hello">
    <div class="login-page1">
      <div class="container-fluid p-0">
        <div class="row">
          <div class="col-12">
      
    <div id="screenShared" class="text-center alert-info alert hidden"></div>

    <div id="install-button"></div>
    <!-- <section id="logs-message" class="experiment"
        style="display: none;text-align: center;font-size: 1.5em;line-height: 2;color: red;">WebRTC getDisplayMedia API.
    </section> -->
    <p id="logs-message">Share your screen</p>

    <section class="experiment">
        <section class="hide-after-join">
            <button id="share-screen" @click="screenShares()" class="btn btn-primary setup text-center">Start Sharing
                Screen </button>
        </section>
        <div id="videosContainer" style=" display:none;"></div>
    </section>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import $ from "jquery";
import JQuery from "jquery";
import "bootstrap";
import feather from "feather-icons";
import Popper from "popper.js";
import Datepicker from 'vuejs-datepicker';
import "feather-icons/dist/feather.min.js";
import tippy from "tippy.js";
import "tippy.js/dist/tippy.css";
// import'../services/viewscreen.js';

import {
  AirplayIcon,
  AtSignIcon,
  PhoneIcon,
  VideoIcon,
  SmileIcon,
  MicIcon,
  SendIcon,
  MessageSquareIcon,
  UsersIcon,
  PlusCircleIcon,
  PlusIcon,
  PhoneIncomingIcon,
  PhoneOutgoingIcon,
  FileIcon,
  ClockIcon,
  ListIcon,
  GridIcon,
  BookIcon,
  XIcon,
  DownloadIcon,
  SearchIcon,
  StarIcon,
  MoreVerticalIcon,
} from "vue-feather-icons";
import carousel from "vue-owl-carousel";

export default {
  name: "Share",
  components: {
    carousel,
    PhoneIncomingIcon,
    PhoneIcon,
    Datepicker,
    VideoIcon,
    SmileIcon,
    MicIcon,
    SendIcon,
    MessageSquareIcon,
    UsersIcon,
    PlusCircleIcon,
    PlusIcon,
    PhoneOutgoingIcon,
    FileIcon,
    ClockIcon,
    ListIcon,
    GridIcon,
    BookIcon,
    XIcon,
    DownloadIcon,
    SearchIcon,
    StarIcon,
    MoreVerticalIcon,
  },
  props: [],
  data() {
    return {
      
    }
  },
  watch: {},
  methods: {
    screenShares(){
          var roomName = document.getElementById('room-name') || {};

    let tokenIs = localStorage.getItem('tokenIs');
    console.log(localStorage.getItem('userData'));
    let currentUserName = localStorage.getItem('userData').name;

    roomName.disabled = true;
    console.log(currentUserName);
    captureUserMedia(function () {
        conferenceUI.createRoom({
            roomName: (currentUserName || 'Anonymous') + ' shared his screen with you',
            roomData: tokenIs
        });
    });
    $("#share-screen").attr("disabled", true);
    this.disabled = true;
    }
  },
  mounted() {
var config = {
    // via: https://github.com/muaz-khan/WebRTC-Experiment/tree/master/socketio-over-nodejs
    openSocket: function (config) {
      
        var SIGNALING_SERVER = 'https://peekvideochat.com:9559/';

        var channel = config.channel || 'peekChatSystem';
        //  var channel = "tocherChatSystem";//config.channel || location.href.replace(/\/|:|#|%|\.|\[|\]/g, '');
        var sender = Math.round(Math.random() * 999999999) + 999999999;

        io.connect(SIGNALING_SERVER).emit('new-channel', {
            channel: channel,
            sender: sender
        });
    
        var socket = io.connect(SIGNALING_SERVER + channel);
        socket.channel = channel;
        
        socket.on('connect', function () {
            if (config.callback) config.callback(socket);
            console.log("Screen share connect");
        });

        socket.send = function (message) {
            socket.emit('message', {
                sender: sender,
                data: message
            });
        };

        socket.on('message', config.onmessage);
    },
    onRemoteStream: function (media) {
        if (isbroadcaster) return;
        console.log("onRemoteStream");
        var video = media.video;
        videosContainer.insertBefore(video, videosContainer.firstChild);
        rotateVideo(video);

        document.querySelector('.hide-after-join').style.display = 'none';

    },
    onRoomFound: function (room) {
    },
    onNewParticipant: function (numberOfParticipants) {
        var text = numberOfParticipants + ' users are viewing your screen!';

        if (numberOfParticipants <= 0) {
            text = 'No one is viewing your screen YET.';
        }
        else if (numberOfParticipants == 1) {
            text = 'Only one user is viewing your screen!';
        }

        document.title = text;
        showErrorMessage(document.title, 'green');
    },
    oniceconnectionstatechange: function (state) {
        var text = '';
        console.log(state);
        if (state == 'closed' || state == 'disconnected') {
            text = 'One of the participants just left.';
            document.title = text;
            showErrorMessage(document.title);
        }

        if (state == 'failed') {
            text = 'Failed to bypass Firewall rules. It seems that target user did not receive your screen. Please ask him reload the page and try again.';
            document.title = text;
            showErrorMessage(document.title);
        }

        if (state == 'connected' || state == 'completed') {
            text = 'A user successfully received your screen.';
            document.title = text;
            showErrorMessage(document.title, 'green');
        }

        if (state == 'new' || state == 'checking') {
            text = 'Someone is trying to join you.';
            document.title = text;
            showErrorMessage(document.title, 'green');
        }
    }
};

function showErrorMessage(error, color) {
     console.log(error);
    $('#logs-message').text(error + '');

}

function getDisplayMediaError(error) {
    if (location.protocol === 'http:') {
        showErrorMessage('Please test this WebRTC experiment on HTTPS.');
    } else {
        showErrorMessage(error.toString());
    }
}

function captureUserMedia(callback) {
    var video = document.createElement('video');
    video.muted = true;
    video.volume = 0;
    try {
        video.setAttributeNode(document.createAttribute('autoplay'));
        video.setAttributeNode(document.createAttribute('playsinline'));
        video.setAttributeNode(document.createAttribute('controls'));
    } catch (e) {
        video.setAttribute('autoplay', true);
        video.setAttribute('playsinline', true);
        video.setAttribute('controls', true);
    }

    if (navigator.getDisplayMedia || navigator.mediaDevices.getDisplayMedia) {
        function onGettingSteam(stream) {
            video.srcObject = stream;
            videosContainer.insertBefore(video, videosContainer.firstChild);

            addStreamStopListener(stream, function () {
                location.reload();
            });

            console.log(config);
            $('#logs-message').text('sharing screen ...');
            config.attachStream = stream;
            callback && callback();
            rotateVideo(video);

            addStreamStopListener(stream, function () {
                location.reload();
            });

           // showPrivateLink();

            document.querySelector('.hide-after-join').style.display = 'none';
        }

        if (navigator.mediaDevices.getDisplayMedia) {
            navigator.mediaDevices.getDisplayMedia({ video: true }).then(stream => {
                onGettingSteam(stream);
            }, getDisplayMediaError).catch(getDisplayMediaError);
        }
        else if (navigator.getDisplayMedia) {
            navigator.getDisplayMedia({ video: true }).then(stream => {
                onGettingSteam(stream);
            }, getDisplayMediaError).catch(getDisplayMediaError);
        }
    }
    else {
        if (DetectRTC.browser.name === 'Chrome') {
            if (DetectRTC.browser.version == 71) {
                showErrorMessage('Please enable "Experimental WebPlatform" flag via chrome://flags.');
            } else if (DetectRTC.browser.version < 71) {
                showErrorMessage('Please upgrade your Chrome browser.');
            } else {
                showErrorMessage('Please make sure that you are not using Chrome on iOS.');
            }
        }

        if (DetectRTC.browser.name === 'Firefox') {
            showErrorMessage('Please upgrade your Firefox browser.');
        }

        if (DetectRTC.browser.name === 'Edge') {
            showErrorMessage('Please upgrade your Edge browser.');
        }

        if (DetectRTC.browser.name === 'Safari') {
            showErrorMessage('Safari does NOT supports getDisplayMedia API yet.');
        }
    }
}

/* on page load: get public rooms */
var conferenceUI = conference(config);

/* UI specific */
var videosContainer = document.getElementById("videosContainer") || document.body;

function screenShare() {

}

function rotateVideo(video) {
    video.style[navigator.mozGetUserMedia ? 'transform' : '-webkit-transform'] = 'rotate(0deg)';
    setTimeout(function () {
        video.style[navigator.mozGetUserMedia ? 'transform' : '-webkit-transform'] = 'rotate(360deg)';
    }, 1000);
}
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style >

.dob input {
      border: none !important;
    background: transparent !important;
    width: 100%;
}
.login-content .form1 .form-group, .login-content .form2 .form-group {
    margin-bottom: 15px;
}
</style>
