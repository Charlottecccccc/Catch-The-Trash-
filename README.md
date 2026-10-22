# Catch-The-Trash-
def on_on_overlap(sprite2, otherSprite2):
    otherSprite2.destroy(effects.fire, 100)
    game.game_over(False)
sprites.on_overlap(SpriteKind.player, SpriteKind.enemy, on_on_overlap)

# If net sprite and trash sprite overlap, trash dissapears (destroyed) and confetti plays
# effects.confetti makes the confetti appear after collision
# info.change_score_by makes the score increase by 1 everytime the trash and net collide
# def is a function

def on_on_overlap2(sprite, otherSprite):
    otherSprite.destroy(effects.confetti, 200)
    info.change_score_by(1)
sprites.on_overlap(SpriteKind.player, SpriteKind.food, on_on_overlap2)

Fish: Sprite = None
Trash: Sprite = None
# set background colour
scene.set_background_color(8)
# Create net sprite
mySprite = sprites.create(img("""
        . . . . . . . . . . . . . . . .
        . . . . d d d d d d d d d d d d
        . . d d d d d . . . d d . . d .
        . d d d . . . . . d d . . d d .
        d d d d d d d . d d d . . d d .
        d d d d . . . d d d . . d d d d
        d . d d . . d d . d d d d . . d
        d d d d d d d . . . d d . . . .
        d d d . d d d . . d d d d . . d
        d d d d d . d d d d . . d d d d
        d d d d . . . d d . . . . d d .
        d . d d . . d d d d . . d d d d
        d d d d . d d d d d d d d . . .
        . d d d d d . . d d d . . d d d
        . . d d d d . . d d d . . d . .
        . . . . d d d d d d d d d d d d
        """),
    SpriteKind.player)
# move the net sprite with the controller. net is defined as mySprite
controller.move_sprite(mySprite)
# Set_stay_in_screen (true) makes sure the net always stays on screen
mySprite.set_stay_in_screen(True)
# try means it will stay on the screen at all times
# velocity is set at -50 ms, meaning the trash moves at a velocity of 50 miliseconds

def on_update_interval():
    global Trash
    # Create Trash sprite
    Trash = sprites.create(img("""
            . . . . 1 1 1 . . . 1 1 1 . . .
            . . . . 1 . 1 . . . 1 . 1 . . .
            . . . . 1 . 1 . . . 1 . 1 . . .
            . . . . 1 . 1 1 1 1 1 . 1 . . .
            . . . . 1 . 1 1 1 1 1 . 1 . . .
            . . . . 1 1 1 2 2 2 1 1 1 . . .
            . . . . 1 1 1 3 1 3 1 1 1 . . .
            . . . . 1 1 2 1 1 1 2 1 1 . . .
            . . . . 1 1 2 1 1 1 2 1 1 . . .
            . . . . 1 1 1 3 1 3 1 1 1 . . .
            . . . . 1 1 1 2 2 2 1 1 1 . . .
            . . . . 1 1 1 1 1 1 1 1 1 . . .
            . . . . 1 1 1 1 1 1 1 1 1 . . .
            . . . . . 1 1 1 1 1 1 1 . . . .
            . . . . . . . . . . . . . . . .
            . . . . . . . . . . . . . . . .
            """),
        SpriteKind.food)
    # Create movement intervals for the trash
    Trash.set_position(80 + mySprite.x, randint(5, 115))
    Trash.vx = -50
game.on_update_interval(3000, on_update_interval)

def on_update_interval2():
    global Fish
    Fish = sprites.create(img("""
            . . . . . . . . . . . . . . . .
            . . . . . . . . c c c c . . . .
            . . . . . . c c d d d d c . . .
            . . . . . c c c c c c d c . . .
            . . . . c c 4 4 4 4 d c c . . .
            . . . c 4 d 4 4 4 4 4 1 c . c c
            . . c 4 4 4 1 4 4 4 4 d 1 c 4 c
            . c 4 4 4 4 1 4 4 4 4 4 1 c 4 c
            f 4 4 4 4 4 1 4 4 4 4 4 1 4 4 f
            f 4 4 4 f 4 1 c c 4 4 4 1 f 4 f
            f 4 4 4 4 4 1 4 4 f 4 4 d f 4 f
            . f 4 4 4 4 1 c 4 f 4 d f f f f
            . . f f 4 d 4 4 f f 4 c f c . .
            . . . . f f 4 4 4 4 c d b c . .
            . . . . . . f f f f d d d c . .
            . . . . . . . . . . c c c . . .
            """),
        SpriteKind.enemy)
    # Create movement intervals for the trash
    Fish.set_position(80 + mySprite.x, randint(5, 115))
    Fish.vx = -50
game.on_update_interval(8000, on_update_interval2)
