<div class="door" on:click={handleClick}>
  <div class="door-inner" class:flipped="{flipped}">
    <div class="door-front" class:flippable>
      <span>
        {number}
      </span>
    </div>
    <div class="door-back">
      <img {src} />
    </div>
  </div>
</div>

<script>
  // dynamic imports sort of don't work properly
  import src1 from '$lib/images/01.png';
  import src2 from '$lib/images/02.png';
  import src3 from '$lib/images/03.png';
  import src4 from '$lib/images/04.png';
  import src5 from '$lib/images/05.png';
  import src6 from '$lib/images/06.png';
  import src7 from '$lib/images/07.png';
  import src8 from '$lib/images/08.png';
  import src9 from '$lib/images/09.png';
  import src10 from '$lib/images/10.png';
  import src11 from '$lib/images/11.png';
  import src12 from '$lib/images/12.png';
  import src13 from '$lib/images/13.png';
  import src14 from '$lib/images/14.png';
  import src15 from '$lib/images/15.png';
  import src16 from '$lib/images/16.png';
  import src17 from '$lib/images/17.png';
  import src18 from '$lib/images/18.png';
  import src19 from '$lib/images/19.png';
  import src20 from '$lib/images/20.png';
  import src21 from '$lib/images/21.png';
  import src22 from '$lib/images/22.png';
  import src23 from '$lib/images/23.png';
  import src24 from '$lib/images/24.png';

  export let number;

  const images = [
    src1, src2, src3, src4, src5, src6, src7, src8, src9,
    src10, src11, src12, src13, src14, src15, src16, src17, src18, src19,
    src20, src21, src22, src23, src24
  ];
  let src = images[number - 1];

  // allow the query param `?day=3` to mock the day when the `VITE_CURRENT_DAY`
  // env variable is set
  let today;
  const dayFromQueryParam = new URLSearchParams(location.search).get('day');
  if (import.meta.env.VITE_OVERRIDABLE_DAY && dayFromQueryParam) {
    today = parseInt(dayFromQueryParam);
  }
  else {
    const date = new Date();
    // only allow december
    if (date.getMonth() + 1 === 12) {
      today = date.getDate();
    }
    else {
      today = 0;
    }
  }

  const flippable = number <= today;

  let flipped;
  if (flippable) {
    flipped = getValues()[number - 1];
  }

  function flip() {
    flipped = true;
    setValues();
  }

  function getValues() {
    return JSON.parse(localStorage.getItem('values')) || Array(24);
  }

  function setValues() {
    const values = getValues();
    values[number - 1] = flipped;
    localStorage.setItem('values', JSON.stringify(values));
  }

  function handleClick(event) {
    if (flippable) {
      flip();
    }
  }
</script>

<style>
.door {
  background: transparent;
  width: 200px;
  height: 200px;
  margin: 1.5px;

  perspective: 1000px;
}

.door-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.8s;
  transform-style: preserve-3d;
}

.flipped {
  background: red;
  color: blue;
  transform: rotateY(180deg);
}
.door-front, .door-back {
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  width: 100%;
  height: 100%;
  border-radius: 3px;
  -webkit-backface-visibility: hidden; /* Safari */
  backface-visibility: hidden;
}

/* Style the front side (fallback if image is missing) */
.door-front {
  background: rgba(211, 47, 47, 0.91) none repeat scroll 0% 0%;

  &.flippable {
    cursor: pointer;
  }
}

/* Style the back side */
.door-back {
  background: #fff;
  transform: rotateY(180deg);
}

img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
</style>
