<template>
  <div class="container" ref="container">
    <div class="col" v-for="(col, index) in columns" :key="index">
      <div
        ref="pic"
        class="pic"
        v-for="item in col.picList"
        :key="item.name"
        :style="{ width: `${imgItemWidth}px`, height: `${item._height}px` }"
      >
        <img :src="item.src" style="width: 100%" />
        <div class="pic-mask" :style="{ height: `${item._height}px` }">
          <div class="pic-name">{{ item.name }}</div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'waterfall',
  data() {
    const imgArr = [
      'https://film-grab.com/wp-content/uploads/2022/07/The-Adjuster-006.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Live-and-Let-Die-061.jpg',
      'https://film-grab.com/wp-content/uploads/2022/07/After-Yang026.jpg',
      'https://film-grab.com/wp-content/uploads/2022/07/The-Worst-Person-in-the-World-001.jpg',
      'https://film-grab.com/wp-content/uploads/2020/10/Zeroville-025.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/Bigger-Than-Life-029.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Diamonds-are-Forever-060.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/Prisoners-of-Ghostland-002.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/Dune-2021-022.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/Celeste-005.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/On-Her-Majestys-Secret-Service-023.jpg',
      'https://film-grab.com/wp-content/uploads/2022/05/NightmareAlley010.jpg',
      'https://film-grab.com/wp-content/uploads/2022/05/Paris-13th010.jpg',
      'https://film-grab.com/wp-content/uploads/2020/10/Taking-Off-019.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/The-Eyes-of-Tammy-Faye-001.jpg',
      'https://film-grab.com/wp-content/uploads/2022/05/CmonCmon019.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/Frighteners-021.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/You-Only-Live-Twice-003.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/In-Which-We-Serve-008.jpg',
      'https://film-grab.com/wp-content/uploads/2022/05/Apollo101_2036.jpg',
      'https://film-grab.com/wp-content/uploads/2022/05/InTheEarth035.jpg',
      'https://film-grab.com/wp-content/uploads/2022/05/3Iron042.jpg',
      'https://film-grab.com/wp-content/uploads/2022/05/Femme-Fatale049.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Thunderball-005.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/The-Card-Counter-032.jpg',
      'https://film-grab.com/wp-content/uploads/2022/05/The-Apartment003.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Goldfinger-015.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/His-House-047.jpg',
      'https://film-grab.com/wp-content/uploads/2021/09/Der-Prozess-004.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/Dillinger-is-Dead-028.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Domain-007.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/From-Russia-With-Love-002.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Master-Z-052.jpg',
      'https://film-grab.com/wp-content/uploads/2019/10/Friday-the-13th-Part-5-056.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/Universal-Soldier-The-Return-003.jpg',
      'https://film-grab.com/wp-content/uploads/2022/05/Intrusion016.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/The-Canterbury-Tales-016.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/Universal-Soldier-008.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Ip-Man-4-047.jpg',
      'https://film-grab.com/wp-content/uploads/2021/10/Shadow-Film-01.jpg',
      'https://film-grab.com/wp-content/uploads/2021/10/Les-Chants-de-Maldoror-011.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/Desert-Hearts-024.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/Straight-Time-005.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Ip-Man-3-006.jpg',
      'https://film-grab.com/wp-content/uploads/2021/09/Emperor-Tomato-Ketchup-020.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Black-Widow-009.jpg',
      'https://film-grab.com/wp-content/uploads/2020/10/Border-006.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/Green-Inferno-029.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/The-Damned-013.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Ip-Man-2-054.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Passing-001.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Master-of-the-House-003.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Outside-Satan-003.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Black-Orpheus-043.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Ip-Man-001.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Last-Night-In-Soho-023.jpg',
      'https://film-grab.com/wp-content/uploads/2021/09/Explorers-039.jpg',
      'https://film-grab.com/wp-content/uploads/2021/10/Me-and-Earl-028.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Annette-014.jpg',
      'https://film-grab.com/wp-content/uploads/2021/10/The-Rubber-05.jpg',
      'https://film-grab.com/wp-content/uploads/2021/10/Hana-Bi-046.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/Oppenheimer-64.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_01.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_02.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_03.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_04.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_05.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_06.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_07.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_08.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_09.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_10.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_10.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_11.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_12.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_13.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_14.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_15.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_16.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_17.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_18.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_19.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_20.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_21.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_22.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_23.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_24.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_25.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_26.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_27.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_28.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_29.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_30.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_31.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_32.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_33.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_34.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_35.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_36.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_37.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_38.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_39.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_40.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_41.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_42.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_43.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_44.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_45.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_46.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_47.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_48.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_49.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_50.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_51.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_52.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_53.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_54.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_55.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_56.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_57.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_58.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_59.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_60.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_61.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_62.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_63.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_64.jpg',
      'https://film-grab.com/wp-content/uploads/photo-gallery/thumb/Oppenheimer_65.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/When-Evil-Lurks-15.jpg',
      'https://film-grab.com/wp-content/uploads/2024/01/ADRTOS-57.jpg',
      'https://film-grab.com/wp-content/uploads/2023/12/Anatomy-of-a-Fall-08.jpg',
      'https://film-grab.com/wp-content/uploads/2023/12/Polite-Society-65.jpg',
      'https://film-grab.com/wp-content/uploads/2023/12/Yentl-17.jpg',
      'https://film-grab.com/wp-content/uploads/2023/12/The-New-Boy-09.jpg',
      'https://film-grab.com/wp-content/uploads/2023/12/Brooklyn-45-42.jpg',
      'https://film-grab.com/wp-content/uploads/2023/12/Dream-Scenario-24.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/Beau-is-Afraid-25.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/Mission-Impossible-Dead-Reckoning-Part-1-62.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/Enys-Men-18.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/ASIB-1976-64.jpg',
      'https://film-grab.com/wp-content/uploads/2024/01/The-Sacrifice-Game-33.jpg',
      'https://film-grab.com/wp-content/uploads/2024/01/HGBOSAS-49.jpg',
      'https://film-grab.com/wp-content/uploads/2023/12/The-Creator-24.jpg',
      'https://film-grab.com/wp-content/uploads/2024/01/Joyland-38.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/El-Conde-41.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/Rye-Lane-15.jpg',
      'https://film-grab.com/wp-content/uploads/2023/12/Ballerina-12.jpg',
      'https://film-grab.com/wp-content/uploads/2024/01/Unwelcome-51.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/Godland-25.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/Mutant-Mayhem-62.jpg',
      'https://film-grab.com/wp-content/uploads/2023/12/Renfield-02.jpg',
      'https://film-grab.com/wp-content/uploads/2024/01/Saltburn-61.jpg',
      'https://film-grab.com/wp-content/uploads/2023/12/Return-To-Seoul-36.jpg',
      'https://film-grab.com/wp-content/uploads/2023/12/Leave-The-World-Behind-28.jpg',
      'https://film-grab.com/wp-content/uploads/2023/12/Kokomo-City-42.jpg',
      'https://film-grab.com/wp-content/uploads/2023/12/Silent-Night-07.jpg',
      'https://film-grab.com/wp-content/uploads/2023/03/Christmas-Bloody-Christmas-20.jpg',
      'https://film-grab.com/wp-content/uploads/2023/12/Maestro-03.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/No-One-Will-Save-You-41.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/Magic-Mikes-Last-Dance-55.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/Birth-Rebirth-22.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/Skinamarink-35.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/Showing-Up-26.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/Past-Lives-45.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/Suitable-Flesh-61.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/They-Cloned-Tyrone-20.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/Across-The-Spider-Verse-30.jpg',
      'https://film-grab.com/wp-content/uploads/2023/12/Killers-of-the-Flower-Moon-03.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/Oppenheimer-64.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/Barbie-59.jpg',
      'https://film-grab.com/wp-content/uploads/2023/12/May-December-35.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/Poison-2023-03.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/The-Ratcatcher-04.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/The-Swan-11.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/Henry-Sugar-33.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/Asteroid-City-10.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/Napoleon-1927-51.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/The-Last-Duel-46.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/Thelma-Louise-06.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/Legend-14.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/The-Duellists-03.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/The-Boogeyman-50.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/Passengers-12.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/Imporrt-Export-61.jpg',
      'https://film-grab.com/wp-content/uploads/2020/09/Harriet-063.jpg',
      'https://film-grab.com/wp-content/uploads/2023/11/The-Killer-02.jpg',
      'https://film-grab.com/wp-content/uploads/2020/09/6-Underground-065.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/The-Many-Saints-of-Newark-038.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Help-035.jpg',
      'https://film-grab.com/wp-content/uploads/2022/05/Dual018.jpg',
      'https://film-grab.com/wp-content/uploads/2020/09/Dark_Waters_058.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/No-Man-Of-God-022.jpg',
      'https://film-grab.com/wp-content/uploads/2022/10/Confess-Fletch-04.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/Broadcast-Signal-Interruption-031.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Halloween-Kills-049.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/Halloween-II-046.jpg',
      'https://film-grab.com/wp-content/uploads/2019/10/The-Predator-037.jpg',
      'https://film-grab.com/wp-content/uploads/2022/07/The-Empty-Man-015.jpg',
      'https://film-grab.com/wp-content/uploads/2019/03/ouija029.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/Fright-Night-006.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/Insidious-Chapter-2-040.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/Insidious-019.jpg',
      'https://film-grab.com/wp-content/uploads/2022/05/YouAreNotMyMother038.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Night-Teeth-033.jpg',
      'https://film-grab.com/wp-content/uploads/2022/05/Hatching011.jpg',
      'https://film-grab.com/wp-content/uploads/2019/10/Friday-the-13th-Part-8-058.jpg',
      'https://film-grab.com/wp-content/uploads/2022/08/After-Blue008.jpg',
      'https://film-grab.com/wp-content/uploads/2023/03/Causeway-31.jpg',
      'https://film-grab.com/wp-content/uploads/2022/08/The-Amazing-Mr-X-017.jpg',
      'https://film-grab.com/wp-content/uploads/2023/03/Bardo-19.jpg',
      'https://film-grab.com/wp-content/uploads/2023/03/Goodnight-Mommy-2022-28.jpg',
      'https://film-grab.com/wp-content/uploads/2023/03/Ghostbusters-Afterlife-33.jpg',
      'https://film-grab.com/wp-content/uploads/2023/03/Babylon-10.jpg',
      'https://film-grab.com/wp-content/uploads/2020/09/Earthquake-Bird-022.jpg',
      'https://film-grab.com/wp-content/uploads/2023/03/Awaken-03.jpg',
      'https://film-grab.com/wp-content/uploads/2022/02/Anna-and-the-Apocalypse-031.jpg',
      'https://film-grab.com/wp-content/uploads/2023/03/Empire-of-Light-17.jpg',
      'https://film-grab.com/wp-content/uploads/2022/08/Live-By-Night-037.jpg',
      'https://film-grab.com/wp-content/uploads/2023/04/Women-Talking-22.jpg',
      'https://film-grab.com/wp-content/uploads/2022/08/Insomnia-027.jpg',
      'https://film-grab.com/wp-content/uploads/2023/04/The-Gift-08.jpg',
      'https://film-grab.com/wp-content/uploads/2023/04/The-Power-of-the-Dog-42.jpg',
      'https://film-grab.com/wp-content/uploads/2021/09/Catalogue-of-Memory-002.jpg',
      'https://film-grab.com/wp-content/uploads/2023/06/Chopper_018.jpg',
      'https://film-grab.com/wp-content/uploads/2023/03/Banshees-of-Inisherin-61.jpg',
      'https://film-grab.com/wp-content/uploads/2023/03/Bones-and-All-49.jpg',
      'https://film-grab.com/wp-content/uploads/2022/08/Beatrice-Cenci035.jpg',
      'https://film-grab.com/wp-content/uploads/2021/09/An-Attempt-to-Describe-008.jpg',
      'https://filmgrab.files.wordpress.com/2016/01/38145.jpg',
      'https://film-grab.com/wp-content/uploads/2023/03/Decision-to-Leave-56.jpg',
      'https://film-grab.com/wp-content/uploads/2021/09/A-Tale-of-Smallpox-001.jpg',
      'https://film-grab.com/wp-content/uploads/2023/03/Phase-4-27.jpg',
      'https://film-grab.com/wp-content/uploads/2023/03/It-is-in-us-all-14.jpg',
      'https://film-grab.com/wp-content/uploads/2023/03/Infinity-Pool-21.jpg',
      'https://film-grab.com/wp-content/uploads/2021/09/Blueberry-021.jpg',
      'https://film-grab.com/wp-content/uploads/2021/09/A-Tale-of-Labyrinth-011.jpg',
      'https://film-grab.com/wp-content/uploads/2017/01/loveontherun044.jpg',
      'https://film-grab.com/wp-content/uploads/2023/03/M3gan-45.jpg',
      'https://film-grab.com/wp-content/uploads/2023/03/Knock-at-the-Cabin-18.jpg',
      'https://film-grab.com/wp-content/uploads/2023/04/The-Silent-Twins-36.jpg',
      'https://film-grab.com/wp-content/uploads/2023/03/Pearl-65.jpg',
      'https://film-grab.com/wp-content/uploads/2022/04/Casino-Royale-029.jpg',
      'https://film-grab.com/wp-content/uploads/2023/04/The-Whale-39.jpg',
    ].map((el) => {
      return {
        src: el,
        name: el.substring(49)
      }
    })
    return {
      imgArr,
      columns: [],
      loadedCount: 0,
      imgItemWidth: 360, // 图片宽度
      gap: 20, // 间隙
      times: null
    }
  },
  async mounted() {
    await this.picLoad()
    this.initData()
    window.onresize = () => {
      if (this.times) {
        clearTimeout(this.times)
      }
      this.times = setTimeout(() => {
        this.initData()
      }, 500)
    }
  },
  methods: {
    picLoad() {
      return new Promise((resolve) => {
        this.imgArr.forEach((item) => {
          if (!item.src) {
            this.loadedCount++
            item['_height'] = 0
            if (this.loadedCount == this.imgArr.length) {
              resolve()
            }
          } else {
            let img = new Image()
            img.src = item.src
            img.onload = () => {
              this.loadedCount++
              item['_height'] = Math.round(this.imgItemWidth * (img.height / img.width))
              if (this.loadedCount == this.imgArr.length) {
                resolve()
              }
            }
            img.onerror = () => {
              this.loadedCount++
              item['_height'] = 0
              if (this.loadedCount == this.imgArr.length) {
                resolve()
              }
            }
          }
        })
      })
    },
    initData() {
      let clientWidth = this.$refs.container.clientWidth, // 页面视图容器宽度
        cols = Math.floor(clientWidth / (this.imgItemWidth + this.gap)), // 计算显示列数
        columns = []
      // 初始每列首行元素
      for (let i = 0; i < cols; i++) {
        this.imgArr[i]['_top'] = 0
        columns.push({ picList: [this.imgArr[i]] })
      }
      // 处理剩余元素
      for (let i = cols; i < this.imgArr.length; i++) {
        let minHeight = this.getMin(columns)
        this.imgArr[i]['_top'] = minHeight.height
        columns[minHeight.index]['picList'].push(this.imgArr[i])
      }
      this.columns = columns
    },
    getMin(columns) {
      let index = 0,
        min = columns.reduce((prev, cur, i) => {
          let _cur = cur.picList[cur.picList.length - 1],
            h = parseInt(_cur._top) + parseInt(_cur._height)
          if (prev == 0) {
            return h
          } else if (h < prev) {
            index = i
            return h
          } else {
            return prev
          }
        }, 0)
      return { height: min, index }
    }
  }
}
</script>

<style lang="scss" scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.container {
  width: 99vw;
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
  padding: 0 20px 20px;
  .pic {
    overflow: hidden;
    border-radius: 10px;
    margin-top: 20px;
    transition: all 0.6s;
    &-mask {
      width: 100%;
      background-color: rgba(0, 0, 0, 0);
      transition: background-color 4s;
      transform: translateY(-100%);
      display: flex;
      align-items: flex-end;
      justify-content: center;
      .pic-name {
        height: 30px;
        text-align: center;
        font-weight: bold;
        color: transparent;
        transform: translateY(30px);
        transition: all 1s;
      }
    }
    &-mask:hover {
      background-color: rgba(0, 0, 0, 0.4);
      transition: background-color 4s linear 0.5s;
      .pic-name {
        color: #fff;
        transform: translateY(0px);
        transition: all 1s;
      }
    }
  }
  .pic:hover {
    transform: translateY(-10px);
    transition: all 0.6s;
  }
}
</style>
