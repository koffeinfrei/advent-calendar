<script>
  import { dev } from '$app/environment';

  export let number;
  const src = `/${('00' + number).slice(-2)}.png`;

  // allow the query param `?day=3` in development mode to mock the day
  let today;
  const dayFromQueryParam = new URLSearchParams(location.search).get('day');
  if (dev && dayFromQueryParam) {
    today = parseInt(dayFromQueryParam);
  }
  else {
    today = (new Date()).getDate();
  }

  let flipped;
  if (number <= today) {
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
    if (number <= today) {
      flip();
    }
  }
</script>

<div class="door" on:click={handleClick}>
  <div class="door-inner" class:flipped="{flipped}">
    <div class="door-front">
      <span>
        {number}
      </span>
    </div>
    <div class="door-back">
      <img {src} />
    </div>
  </div>
</div>

<style>
.door {
  background: transparent;
  width: 200px;
  height: 200px;
  margin: 0.5px;

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
  cursor: pointer;
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
