<!DOCTYPE html>
<html>
<head>
  <title>Battle Dude IO</title>
  <script src="https://cdn.jsdelivr.net/npm/phaser@3/dist/phaser.min.js"></script>
</head>
<body>
  <script>
    const config = {
      type: Phaser.AUTO,
      width: 800,
      height: 600,
      physics: {
        default: 'arcade',
        arcade: { debug: false }
      },
      scene: {
        preload: preload,
        create: create,
        update: update
      }
    };

    const game = new Phaser.Game(config);

    let player, cursors;

    function preload() {
      this.load.image('player', 'https://example.com/player.png'); // 플레이어 이미지 URL
      this.load.image('bullet', 'https://example.com/bullet.png'); // 총알 이미지 URL
    }

    function create() {
      player = this.physics.add.sprite(400, 300, 'player');
      player.setCollideWorldBounds(true);

      cursors = this.input.keyboard.createCursorKeys();

      this.input.on('pointerdown', () => {
        const bullet = this.physics.add.sprite(player.x, player.y, 'bullet');
        this.physics.moveTo(bullet, this.input.x, this.input.y, 500);
      });
    }

    function update() {
      player.setVelocity(0);

      if (cursors.left.isDown) player.setVelocityX(-200);
      if (cursors.right.isDown) player.setVelocityX(200);
      if (cursors.up.isDown) player.setVelocityY(-200);
      if (cursors.down.isDown) player.setVelocityY(200);
    }
  </script>
</body>
</html>

