<script>
const randomColor = () => {
  const colors = [
    "#93C5FD", // Bleu pastel
    "#A5B4FC", // Indigo doux
    "#C4B5FD", // Lavande doux
    "#D8B4FE", // Mauve pastel
    "#F0ABFC", // Rose doux
  ];

  const randomIndex = Math.floor(Math.random() * colors.length);
  return colors[randomIndex];
};

export { randomColor };
</script>
