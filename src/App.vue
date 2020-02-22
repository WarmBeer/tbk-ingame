<template>
  <div id="app">
    <div class="browser-wrapper">
      <div class="header">
        <div class="upper-header">
          <div class="header-text">SERVER BROWSER</div>
          <div class="header-functions">
            <input id="server-list-filter" type="text" placeholder="Search.." v-model="query">
            <button id="refresh" class="btn-refresh" @click="refresh()">Refresh</button>
          </div>
        </div>
        <div class="bottom-header">
          <div class="header-info">
            <span class="server-info">{{ totalPlayers }} PLAYERS ONLINE</span>
          </div>
          <div class="header-filters">
          </div>
        </div>
      </div>
      <div id="server-list-wrap">
        <ServerList
        :servers="servers"
        >
        </ServerList>
      </div>
    </div>
  </div>
</template>

<script>

import ServerList from "@/components/ServerList";
export default {
  name: 'App',
  components: {ServerList},
  data() {
    return {
      query: '',
      servers: [],
      isRefreshing: false,
      totalPlayers: 0,
    }
  },
  methods: {
    refresh() {
      this.isRefreshing = true;
      fetch('https://halokeg.net/api/messages')
              .then(response => response.json())
              .then((result) => {
                this.servers = result;
                this.isRefreshing = false;
              });
      fetch('https://halokeg.net/api/players')
              .then(response => response.json())
              .then((result) => {
                this.totalPlayers = result;
              });
    },
    getClass(){
      return this.isRefreshing ? "refreshing" : "";
    },
  },
  mounted() {
    this.refresh();
  }
}
</script>

<style>

  html, body {
    width: 100%;
    height: 100%;
    margin: 0;
    overflow: hidden;
  }

  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
  }

  #server-list-wrap {
  }

  .browser-wrapper {
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    padding: 2% 12%;
    background: linear-gradient(rgba(0,26,53,.9),rgba(0,26,53,.8))
  }

  .header {
    margin: 1% 0;
  }

  .upper-header {
    justify-content: space-between;
    display: flex;
    margin-bottom: 1%;
  }

  .bottom-header {
    justify-content: space-between;
    display: flex;
  }

  .toggle-view {
    width: 12vw;
    background-color: rgba(255,255,255, 0.25);
    border: none;
    border-radius: 24px;
    font-size: 1vw;
    color: white;
    margin: 1% 0;
    margin-right: 4%;
    outline: none;
  }

  .header-text {
    font-size: 2vw;
    letter-spacing: 0.6vw;
    color: rgba(255, 255, 255, 1.0);
    font-weight: 700;
  }

  .header-info {
    color: rgb(249, 159, 28);
    font-size: 1.2vw;
    font-weight: bold;
    justify-content: space-between;
    display: flex;
    float: left;
  }

  .header-filters {
    justify-content: space-between;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    float: right;
    width: 50%;
  }

  .header-filters button {
    background-color: transparent;
    border-radius: 24px;
    border: none;
    padding: 8px 0px;
    width: calc(1/6*100% - (1 - 1/6)*10px);
    display:inline-block;
    cursor:pointer;
    color:#ffffff;
    text-decoration:none;
    font-size: 1vw;
    font-weight: 500;
    color: rgba(255, 255, 255, 0.9);
    outline:none;
    transition: 0.25s ease-in-out;
  }

  .header-filters button:hover {
    color: rgba(255, 255, 255, 1);
  }

  .header-filters button.active {
    background-color: rgba(255,255,255, 0.25);
  }

  .server-list {
    width: 100%;
    table-layout: fixed;
    border-collapse: collapse;
  }

  .server-list th:nth-child(1), .server-list td:nth-child(1){ width: 10%;}
  .server-list th:nth-child(2), .server-list td:nth-child(2){ width: 20%;}
  .server-list th:nth-child(3), .server-list td:nth-child(3){ width: 10%;}
  .server-list th:nth-child(4), .server-list td:nth-child(4){ width: 30%;}
  .server-list th:nth-child(5), .server-list td:nth-child(5){ width: 10%;}
  .server-list th:nth-child(6), .server-list td:nth-child(6){ width: 10%;}
  .server-list th:nth-child(7), .server-list td:nth-child(6){ width: 10%;}

  .server-list tr {
    font-size: 0.9vw;
    color: rgba(255, 255, 255, 1);
    display: table-row;
  }

  .server-list > tbody > tr > td {
    display: table-cell;
    align-items:center;
    overflow: hidden;
    text-overflow: ellipsis;
    text-align: left;
  }

  .server-list > thead {
    font-size: 1vw;
    background: rgba(255, 255, 255, 0.15);
    border-radius: 0px;
    width: 100%;
    display: table-header-group;
    color: rgba(255, 255, 255, 0.75);
    text-transform: uppercase;
  }

  .server-list > thead > tr > th {
    padding: 10px 0;
    padding-left: 10px;
    text-align: left;
  }

  .server-list > thead > tr > th:hover {
    color: rgba(255, 255, 255, 1);
  }

  .server-list > tbody {
    display:table-row-group;
    height: 70vh;
    overflow: hidden;
    overflow-y: auto;
  }

  .header-functions {
    justify-content: space-between;
    display: flex;
    float: right;
  }

  .icon {
    height: 1.25vw;
    width: auto;
  }

  .lock {
    height: 1.15vw;
    width: auto;
  }

  /*Server list detailed*/

  .server-list-detailed {
    display: block;
    height: 70vh;
    overflow: hidden;
    overflow-y: auto;
  }

  .server-detailed {
    width: 100%;
    height: 8vw;
    font-size: 0.8vw;
    box-sizing: border-box;
    font-weight: 300;
    color: rgba(255, 255, 255, 0.85);
    border-left: 6px solid transparent;
    -webkit-transition: 0.5s;
    -moz-transition: 0.5s;
    transition: 0.5s;
    display: inline-block;
    overflow: hidden;
    text-overflow: ellipsis;
    padding: .5% 1%;
  }

  .server-detailed:hover {
    background-color: rgba(240,248,255, 0.2);
    color: rgba(255, 255, 255, 1);
    border-left-color: rgba(240,248,255, 0.65);
  }

  .server-detailed > div {
    float: left;
  }

  .server-detailed .map-image, .server-detailed .server-detailed-info {
    display: inline-block;
    box-sizing: border-box;
    white-space: nowrap;
    position: relative;
    top: 50%;
    transform: translateY(-50%);
  }

  .server-detailed .map-image {
    text-align: center;
    width: 22%;
  }

  .server-detailed .map-image img {
    border: 2px solid rgba(255, 255, 255, 0.9);
    width: 100%;
    height: auto;
  }

  .server-detailed .server-detailed-info,  .server-detailed .server-detailed-stats {
    display: inline-block;
    margin-left: 1%;
    width: 34%;
    height: auto;
    vertical-align: middle;
  }

  .server-detailed .server-detailed-stats {
    width: 6%;
    display: grid;
    grid-template-columns: 100%;
    grid-template-rows: 25% 25% 25% 25%;
    height: 100%;
  }

  .server-detailed .server-detailed-stats button {
    width: 100%;
    padding: 5px;
    font-size: 0.8vw;
    border: 2px solid rgba(255, 255, 255, 0.4);
    border-radius: 4px;
    background-color: rgba(255, 255, 255, 0.1);
    outline: none;
  }

  .server-detailed .server-detailed-stats span {
    font-weight: 400;
    font-size: 1vw;
    text-align: right;
    width: 100%;
    white-space: nowrap;
    text-overflow: ellipsis;
    display: block;
    overflow: hidden
  }

  .server-detailed-grid-wrapper {
    margin-left: 1%;
    display: inline-block;
    width: 35%;
  }

  .server-detailed .server-detailed-info span {
    padding: 0 0px;
    font-weight: 400;
    font-size: 1vw;
    text-align: left;
    vertical-align: center;
    width: 100%;
    white-space: nowrap;
    text-overflow: ellipsis;
    display: block;
    overflow: hidden
  }

  .server-detailed-info span.name {
    font-size: 1.1vw;
    font-weight: bold;
  }

  .server-detailed-players {
    display: grid;
    grid-template-columns: 25% 25% 25% 25%;
    grid-template-rows: 25% 25% 25% 25%;
    width: 100%;
    height: 100%;
  }

  .server-detailed-players > div {
    padding: 1px;
    margin: 4px;
    text-align: center;
    color: white;
    border-radius: 1px;
    font-weight: 400;
    text-shadow: 1px 1px black;
    opacity: 0.9;
    white-space: nowrap;
    text-overflow: ellipsis;
    display: block;
    overflow: hidden;
    background-color: rgba(255,255,255,0.1)!important;
  }

  /*Search*/
  #server-list-filter {
    background: url(assets/search.svg) no-repeat;
    background-color: rgba(255, 255, 255, 0.15);
    font-size: 0.9vw;
    color: white;
    padding: 0 0.6vw;
    padding-left: 14%;
    outline: none;
    margin-right: 4%;
    width: 16vw;
    border: 1px solid rgba(255,255,255,0.3);
    background-size: auto 50%;
    background-position: 5% 50%;
  }

  #server-list-filter:focus{
    color: white;
  }

  /* Let's get this party started */
  ::-webkit-scrollbar {
    width: 12px;
  }

  /* Track */
  ::-webkit-scrollbar-track {
    background-color: rgba(38, 50, 65, 0.075);
    width: 8px;
  }

  /* Handle */
  ::-webkit-scrollbar-thumb {
    background-color: rgba(255, 255, 255, 0.85);
    width: 8px;
    border-radius: 8px;
  }
  ::-webkit-scrollbar-thumb:hover {
    background-color: rgba(255, 255, 255, 1);
  }
  ::-webkit-scrollbar-thumb:window-inactive {
    background: rgb(98, 106, 116);
  }

  ::placeholder { /* Chrome, Firefox, Opera, Safari 10.1+ */
    color: rgba(255, 255, 255, 0.75);
    opacity: 0.75; /* Firefox */
  }

  .page_footer a:hover {
    text-decoration: underline;
  }

  .toggle-view:hover {
    box-shadow: 0 2px 10px 0 rgba(255, 255, 255, 0.2);
  }

  .btn-refresh {
    padding: 0.6vw 1.2vw;
    border: 1px inset hsla(0,0%,100%,.02);
    text-align: center;
    font-weight: lighter;
    color: hsla(0,0%,100%,1);
    background: hsla(0,0%,100%,.15);
    -webkit-transition: .2s ease-in-out;
    transition: .2s ease-in-out;
    text-decoration: none;
    font-size: 0.9vw;
    outline: none;
  }

  .btn-refresh:hover {
    color: hsla(0,0%,100%,1);
    background: hsla(0,0%,100%,.2);
  }

</style>
