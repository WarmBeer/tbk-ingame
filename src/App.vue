<template>
  <div id="app">
    <div class="browser-wrapper">
      <div class="header">
        <div class="upper-header">
          <div class="header-text">SERVER BROWSER</div>
          <div class="header-functions">
            <input id="server-list-filter" type="text" placeholder="Search.." v-model="query">
            <button id="refresh" :class="getClass()" @click="refresh()">Refresh</button>
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
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
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
      fetch('https://halokeg.net/api/messages')
              .then(response => response.json())
              .then((result) => {
                this.servers = result;
                console.log(result);
              });
    },
    getClass(){
      return this.isRefreshing ? "refreshing" : "";
    },
  },
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
    padding: 1% 4% 5% 5%;
    background-color: rgba(0, 0, 0, 0.5);
  }

  .header {
    margin: 1%;
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
    font-weight: 500;
    font-size: 2.55vw;
    letter-spacing: 1.1vw;
    color: rgba(255, 255, 255, 1.0);
    -webkit-font-smoothing: none;
    font-style: normal;
    text-decoration: none;
    transform: scaleY(1.06);
    float: left;
  }

  .header-info {
    color: coral;
    font-size: 1.2vw;
    font-weight: 500;
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

  .server-list th:nth-child(1), .server-list td:nth-child(1){ width: 2%;}
  .server-list th:nth-child(2), .server-list td:nth-child(2){ width: 2%;}
  .server-list th:nth-child(3), .server-list td:nth-child(3){ width: 41%;}
  .server-list th:nth-child(4), .server-list td:nth-child(4){ width: 15%;}
  .server-list th:nth-child(5), .server-list td:nth-child(5){ width: 10%;}
  .server-list th:nth-child(6), .server-list td:nth-child(6){ width: 10%;}
  .server-list th:nth-child(7), .server-list td:nth-child(7){ width: 8%;}
  .server-list th:nth-child(8), .server-list td:nth-child(8){ width: 7%;}
  .server-list th:nth-child(9), .server-list td:nth-child(9){ width: 5%;}

  .server-list > tbody > tr {
    font-size: 1vw;
    color: rgba(255, 255, 255, 0.9);
    width: calc(100% - 6px);
    border-left: 4px solid transparent;
  }

  .server-list > tbody > tr:hover {
    /*
    background-color: rgba(240,248,255, 0.2);
    color: rgba(255, 255, 255, 1);
    border-left-color: rgba(240,248,255, 0.4);
     */
    background: -webkit-radial-gradient(80%, circle, rgba(199,128,58,0.45) 0%,rgba(211,125,38,0.6) 100%);
    color: rgba(255, 255, 255, 1.0);
    border-left-color: rgba(199,125,58,0.9);
    -webkit-animation: menu-entry-background-pulse 2.5s ease infinite;
  }

  .server-list > tbody > tr > td {
    display: flex;
    align-items:center;
    padding: 15px 0;
    padding-left: 10px;
    overflow: hidden;
    text-overflow: ellipsis;
  }

  .server-list > thead {
    font-size: 1vw;
    background: rgba(255, 255, 255, 0.15);
    border-radius: 0px;
    width: 100%;
    display: block;
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
    display:block;
    height: 70vh;
    overflow: hidden;
    overflow-y: auto;
  }
  .server-list > thead, .server-list > tbody > tr {
    display:table;
    width:100%;
    table-layout:fixed;/* even columns width , fix width of table too*/
  }

  .server-list > thead {
    width: 99.35%;
    margin-left: 4px;
  }

  table.server-list thead tr, .server-list tbody tr {
    display: flex;
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
    font-size: 1.2vw;
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
    font-size: 1.2vw;
    text-align: left;
    vertical-align: center;
    width: 100%;
    white-space: nowrap;
    text-overflow: ellipsis;
    display: block;
    overflow: hidden
  }

  .server-detailed-info span.name {
    font-size: 1.2vw;
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
    background-color: rgba(0,0,0, 0.15);
    font-size: 1vw;
    color: white;
    padding: 0px 12px;
    padding-left: 8%;
    outline: none;
    border-radius: 24px;
    margin-right: 4%;
    width: 20vw;
    border: 3px solid rgba(255,255,255,0.15);
    background-size: auto 50%;
    background-position: 5% 50%;
  }

  #server-list-filter:focus{
    color: white;
  }

  button#refresh:hover {
    opacity: 1;
  }
  button#refresh {
    width: 2.8vw;
    height: 2.8vw;
    font-size: 0;
    background: none;
    border: none;
    background-image: url(assets/icon-refresh.svg);
    background-repeat: no-repeat;
    background-size: 100% 100%;
    /* top: 0; */
    vertical-align: top;
    margin-top: 5px;
    outline: none;
    opacity: 0.8;
  }
  button#refresh.refreshing{
    opacity: 1;
    animation-name: refreshing;
    animation-duration: 1000ms;
    animation-iteration-count: infinite;
    animation-timing-function: linear;
  }
  @keyframes refreshing {
    from {
      transform:rotate(0deg);
    }
    to {
      transform:rotate(360deg);
    }
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

</style>
