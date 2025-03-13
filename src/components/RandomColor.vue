<script>
const randomColor = () => {
  const colors = [
    "#FF5252", //rose
    "#448AFF", //bleu
    "#4CAF50", //vert
    "#ffc823", //jaune
  ];
  const randomIndex = Math.floor(Math.random() * colors.length);
  return colors[randomIndex];
};

export { randomColor };
</script>
