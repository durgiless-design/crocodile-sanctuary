const cards = document.querySelectorAll('.croc-card');
const selectedName = document.getElementById('selectedName');
const selectedWeight = document.getElementById('selectedWeight');
const selectedAge = document.getElementById('selectedAge');
const selectedDimension = document.getElementById('selectedDimension');
const selectedHealth = document.getElementById('selectedHealth');
const selectedStory = document.getElementById('selectedStory');
const harpoonCursor = document.getElementById('harpoonCursor');

function updateSelectedCard(card) {
  cards.forEach((c) => {
    c.classList.remove('is-selected', 'flee');
  });

  card.classList.add('is-selected');

  const others = [...cards].filter((c) => c !== card);
  others.forEach((c) => c.classList.add('flee'));

  selectedName.textContent = card.dataset.name;
  selectedWeight.textContent = card.dataset.weight;
  selectedAge.textContent = card.dataset.age;
  selectedDimension.textContent = card.dataset.dimension;
  selectedHealth.textContent = card.dataset.health;
  selectedStory.textContent = card.dataset.story;

  const pulse = card.querySelector('.pulse');
  if (pulse) {
    pulse.style.animation = 'none';
    void pulse.offsetWidth;
    pulse.style.animation = '';
  }
}

cards.forEach((card) => {
  card.addEventListener('click', () => updateSelectedCard(card));
});

document.addEventListener('pointermove', (event) => {
  harpoonCursor.style.left = `${event.clientX + 8}px`;
  harpoonCursor.style.top = `${event.clientY + 8}px`;
  harpoonCursor.classList.add('visible');
});

document.addEventListener('pointerleave', () => {
  harpoonCursor.classList.remove('visible');
});

document.addEventListener('pointerdown', () => {
  harpoonCursor.style.transform = 'translate(-18px, -18px) rotate(28deg) scale(0.96)';
});

document.addEventListener('pointerup', () => {
  harpoonCursor.style.transform = 'translate(-18px, -18px) rotate(15deg)';
});
