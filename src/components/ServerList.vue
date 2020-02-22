<template>
    <table width="100%" class="server-list">
        <thead>
        <tr>
            <th>Server</th>
            <th></th>
            <th>Host</th>
            <th>Info</th>
            <th>Gamemode</th>
            <th>Playtime</th>
            <th></th>
        </tr>
        </thead>
        <tbody>
        <tr
        v-for="(server, index) in servers"
        :key="index"
        :server="server"
        @click="onClick(server.ip)">
            <td class="td_icon"><img class="icon" :src="server.imageURL"></td>
            <td>{{ server.server }}</td>
            <td>{{ server.host }}</td>
            <td>{{ server.message }}</td>
            <td>{{ server.gamemode }}</td>
            <td>{{ timeSince(Date.parse(server.created)) }}</td>
            <td><a class="btn" :href="'http://thebeerkeg.net/invite/' + server.invite">Join Game</a></td>
        </tr>
        </tbody>
    </table>
</template>

<script>
  export default {
    name: "ServerList",
    props: ['servers'],
    methods: {
      timeSince(date) {
        const seconds = Math.floor((new Date() - date) / 1000);
        let interval = Math.floor(seconds / 31536000);

        if (interval > 1) {
          return `${interval} years`;
        }
        interval = Math.floor(seconds / 2592000);
        if (interval > 1) {
          return `${interval} months`;
        }
        interval = Math.floor(seconds / 86400);
        if (interval > 1) {
          return `${interval} days`;
        }
        interval = Math.floor(seconds / 3600);
        if (interval > 1) {
          return `${interval} hours`;
        }
        interval = Math.floor(seconds / 60);
        if (interval > 1) {
          return `${interval} minutes`;
        }
        return `${Math.floor(seconds)} seconds`;
      },
    },
  }
</script>

<style scoped>
    td, th {
        padding: 0.6vw!important;
    }

    tbody tr {
        background: rgba(255, 255, 255, 0.05);
    }

    .btn {
        padding: 0.6vw;
        border: 1px inset hsla(0,0%,100%,.02);
        text-align: center;
        font-weight: lighter;
        color: rgba(154,171,196,.85);
        background: hsla(0,0%,100%,.15);
        -webkit-transition: .2s ease-in-out;
        transition: .2s ease-in-out;
        text-decoration: none;
    }

    .btn:hover {
        color: hsla(0,0%,100%,1);
        background: hsla(0,0%,100%,.2);
    }

    .icon {
        max-width: 100%;
        max-height: 100%;
        height: auto;
        margin: auto;
    }
</style>
