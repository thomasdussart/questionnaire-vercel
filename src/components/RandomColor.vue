<script>
const randomColor = () => {
  const colors = ["#FF5252", "#448AFF", "#4CAF50", "#ffc823"];
  const randomIndex = Math.floor(Math.random() * colors.length);
  return colors[randomIndex];
};

export { randomColor };
</script>
