<template>
  <div class="flex flex-col justify-center items-center h-[100vh] gap-6">
    <h1 class="text-3xl font-semibold text-[#ffaa0099]">Detect & Translate</h1>
    <form
      @submit.prevent="translate"
      class="relative border-black border-2 rounded-full w-3/4 max-w-[550px] mb-8"
    >
      <input
        type="text"
        v-model="raw"
        placeholder="How can I help You ?"
        class="focus:outline-none p-2 w-full rounded-full pr-12"
        @keyup="translate"
      />
      <button
        class="absolute z-10 right-0 top-0 h-full flex justify-center items-center aspect-square rounded-full bg-[#fa0]"
        type="submit"
      >
        <img
          src="./assets/translation.png"
          alt="translate"
          class="h-[60%] invert"
        />
      </button>
      <span class="absolute right-0 bottom-0 flex translate-y-[120%]">
        translate into :
        <select
          class="border rounded-full cursor-pointer"
          name="languages"
          id="languages"
          v-model="targetLang"
        >
          <option value="af">Afrikaans</option>
          <option value="ar">Arabic</option>
          <option value="bg">Bulgarian</option>
          <option value="ca">Catalan</option>
          <option value="cs">Czech</option>
          <option value="da">Danish</option>
          <option value="de">German</option>
          <option value="el">Greek</option>
          <option value="en" selected>English</option>
          <option value="es">Spanish</option>
          <option value="et">Estonian</option>
          <option value="fi">Finnish</option>
          <option value="fr">French</option>
          <option value="he">Hebrew</option>
          <option value="hi">Hindi</option>
          <option value="hr">Croatian</option>
          <option value="hu">Hungarian</option>
          <option value="id">Indonesian</option>
          <option value="it">Italian</option>
          <option value="ja">Japanese</option>
          <option value="ko">Korean</option>
          <option value="lt">Lithuanian</option>
          <option value="lv">Latvian</option>
          <option value="ms">Malay</option>
          <option value="nl">Dutch</option>
          <option value="no">Norwegian</option>
          <option value="pl">Polish</option>
          <option value="pt">Portuguese</option>
          <option value="ro">Romanian</option>
          <option value="ru">Russian</option>
          <option value="sk">Slovak</option>
          <option value="sl">Slovenian</option>
          <option value="sr">Serbian</option>
          <option value="sv">Swedish</option>
          <option value="th">Thai</option>
          <option value="tr">Turkish</option>
          <option value="uk">Ukrainian</option>
          <option value="vi">Vietnamese</option>
          <option value="zh">Chinese</option>
        </select>
      </span>
    </form>
    <div class="w-4/5 max-w-[600px] mb-8">{{ res }}</div>
  </div>
</template>

<script>
export default {
  mounted() {},
  data() {
    return {
      raw: null,
      res: null,
      targetLang: "en",
    };
  },
  methods: {
    translate() {
      if (this.raw) {
        try {
          fetch(
            `https://simple-translate2.p.rapidapi.com/translate?source_lang=auto&target_lang=${this.targetLang}`,
            {
              method: "POST",
              headers: {
                "x-rapidapi-key":
                  "c8bc5eba24msh8516b52547225b4p1646dejsn673ae40d620e",
                "x-rapidapi-host": "simple-translate2.p.rapidapi.com",
                "Content-Type": "application/json",
              },
              body: JSON.stringify({
                sourceText: this.raw,
              }),
            }
          )
            .then((res) => {
              return res.json();
            })
            .then((response) => {
              this.res = response["data"]["targetText"];
            });
        } catch (error) {
          console.error(error);
        }
      } else {
        this.res = null;
      }
    },
  },
};
</script>

<style></style>
