# Projeto

#-------------------------------------------------------------------------------
# * [ACE] Sapphire Action System IV
#-------------------------------------------------------------------------------
# * By Khas Arcthunder - arcthunder.site40.net
# * Version: 4.4 EN
# * Released on: 11/07/2012
#
#-------------------------------------------------------------------------------
# * Terms of Use
#-------------------------------------------------------------------------------
# Terms of Use – June 22, 2012
# 1. You must give credit to Khas;
# 2. All Khas scripts are licensed under a Creative Commons license
# 3. All Khas scripts are free for non-commercial projects. If you need some 
#    script for your commercial project, check bellow these terms which 
#    scripts are free and which scripts are paid for commercial use;
# 4. All Khas scripts are for personal use, you can use or edit for your own 
#    project, but you are not allowed to post any modified version;
# 5. You can’t give credit to yourself for posting any Khas script;
# 6. If you want to share a Khas script, don’t post the script or the direct 
#    download link, please redirect the user to http://arcthunder.site40.net/
# 7. You are not allowed to convert any of Khas scripts to another engine, 
#    such converting a RGSS3 script to RGSS2 or something of that nature.
# 8. Its your obligation (user) to check these terms on the date you release 
#    your game. Your project must follow them correctly.
#
# Free commercial use scripts:
# - Sapphire Action System IV (RPG Maker VX Ace)
# - Awesome Light Effects (RPG Maker VX Ace)
# - Pixel movement (RPG Maker VX e RPG Maker VX Ace)
# - Sprite & Window Smooth Sliding (RPG Maker VX e RPG Maker VX Ace)
# - Pathfinder (RPG Maker VX Ace)
#
# Check all the terms at http://arcthunder.site40.net/terms/
#
#-------------------------------------------------------------------------------
# * Features
#-------------------------------------------------------------------------------
# The Sapphire Action System IV includes the following features:
# - Pixel Movement
# - Khas Particle Engine powered
# - Realistic collisions
# - Awesome jogability
# - High customization level
# - Weapon Icon
# - Easy to use
# - Skill support
# - Lag free
# - Damage Sprite system
# - Optimized HUD
# - Voice support
# - And more...
#
#-------------------------------------------------------------------------------
# * Instructions
#-------------------------------------------------------------------------------
# All the instructions are on SAS IV guide. Please read them carefully.
#
#-------------------------------------------------------------------------------
# * How to use
#-------------------------------------------------------------------------------
# 1. Physics System
# In order to run this script with the best performance, there's a system 
# called "Physics". This system will load each map between the transitions,
# so you may experience little loadings. The Khas Pixel Movement is not 
# recommended for huge maps.
#
# 2. Event Commands (place a comment)
# There are two special commands for events, you may add a comment with
# the following sintax:
#
# a. [collision_x A]
# This command sets the x collision to A (A must be an integer)
#
# b. [collision_y B]
# This command sets the y collision to B (B must be an integer)
#
# Please check the demo to understand how the collision system works!
#
# 3. Event Commands (call script)
# You can call the following commands for the player or the events
#
# character.px
# This command returns the pixel coordinate X (4 px = 1 tile)
#
# character.py
# This command returns the pixel coordinate Y (4 py = 1 tile)
#
# character.pixel_passable?(px,py,d)
# This command checks the pixel passability from (px, py) to the direction d.
# 
# 4. Map Commands
# You can call a special command to update the passability of the current
# map. You MUST run this command if the option "Auto_Refresh_Tile_Events"
# is set to false.
#
# "But when do I need to use this command?"
# Well, if you change a event graphic to a tileset graphic, or if you remove
# this event graphic, then your map need to be updated!
#
# $game_map.refresh_table(start_x,start_y,end_x,end_y)
#
# Where:
# start_x => Initial X
# start_y => Initial Y
# end_x => End X
# end_y => End Y
#
#-------------------------------------------------------------------------------
# * Warning!
#-------------------------------------------------------------------------------
# Check your tileset directions. If any direction is set as unpassable, the
# system will set the whole tile as unpassable. Setup your tilesets before
# using them!
#
#-------------------------------------------------------------------------------
# * Setup Part (Sapphire Engine)
#-------------------------------------------------------------------------------
module Sapphire_Core
  
  # Enable voice?
  Enable_Voice = true
  
  # Voice files (separated by commas)
  Voice_Files = []
  
  # Voice volume
  Voice_Volume = 80
  
  # Disarmed animation
  Default_Animation = 1
  
  # Default recover time
  Default_Recover = 60
  
  # Switch that will be activated when player dies
  Kill_Switch = 3
  
  # Random factor
  Damage_Random = 0.1
  
  # Enable weapon icon drawing?
  Enable_Weapon_Graphics = true
  
  # Default skill speed
  Default_Skill_Speed = 5
  
  # Default skill recover time
  Default_Skill_Recover = 30
  
  # Skill volume
  Skill_Volume = 80
  
  # Default skill blend type
  Default_Particle_Blend = 1
  
  # Default enemy view range, in virtual pixels (1 tile = 4 virtual pixels)
  Enemy_View = 20
  
  # Enemies' default nature
  # 0 -> Only attack
  # 1 -> Attack and cast skills
  # 2 -> Only cast skills
  Enemy_Nature = 1
  
  # Default enemies' recover time
  Enemy_Recover = 60
  
  # Enable animation when player is seen
  Enemy_Exclamation = true
  
  # Minimal distance to use skills, in virtual pixels (1 tile = 4 virtual pixels)
  Enemy_Skill_Distance = 6
  
  
  # System constant - DO NOT CHANGE!
  Local_Switch = ["A","B","C","D"]
  
  # System constant - DO NOT CHANGE!
  Weapon_Range = {2=>[0,2],4=>[-2,0],6=>[2,0],8=>[0,-2]}
end
#-------------------------------------------------------------------------------
# * Setup Part (Pixel Movement)
#-------------------------------------------------------------------------------
module Pixel_Core
  
  # Auto Update events with tileset graphics?
  Auto_Refresh_Tile_Events = true
  
  # Auto Update range
  TileEvent_Range = 3
  
  # Auto Multiply event commands?
  # (this option will multiply the event commands by 4 if set to true)
  Multiply_Commands = true
  
  # Commands to multiply (ID)
  Commands = [1,2,3,4,5,6,7,8,9,10,11,12,13]
  
#-------------------------------------------------------------------------------
# * Constants - Do not modify!
#-------------------------------------------------------------------------------
  Pixel = 4
  Tile = 0.25
  Default_Collision_X = 3
  Default_Collision_Y = 3
  Body_Axis = [0.25,0.25,0.5,0.75]
  Bush_Axis = [0.5,0.75]
  Counter_Axis = [0.25,0.25,0.25,0.25]
  Ladder_Axis = [0.25,0.25]
  Pixel_Range = {2=>[0,0.25],4=>[-0.25,0],6=>[0.25,0],8=>[0,-0.25]}
  Tile_Range = {2=>[0,1],4=>[-1,0],6=>[1,0],8=>[0,-1]}
  Water_Range = {2=>[0,3],4=>[-3,0],6=>[3,0],8=>[0,-3]}
  Trigger_Range = {2=>[0,2],4=>[-2,0],6=>[2,0],8=>[0,-2]}
  Counter_Range = {2=>[0,3],4=>[-3,0],6=>[3,0],8=>[0,-3]}
  Chase_Axis = {2=>[0,1],4=>[1,0],6=>[1,0],8=>[0,1]}
end
#-------------------------------------------------------------------------------
# * Register
#-------------------------------------------------------------------------------
if $khas_awesome.nil?
  $khas_awesome = []
else
  scripts = []
  $khas_awesome.each { |script| scripts << script[0] }
  if scripts.include?("Pixel Movement")
    error = Sprite.new
    error.bitmap = Bitmap.new(544,416)
    error.bitmap.draw_text(0,208,544,32,"Please remove the script Khas Pixel Movement",1)
    continue = Sprite.new
    continue.bitmap = Bitmap.new(544,416)
    continue.bitmap.font.color = Color.new(0,255,0)
    continue.bitmap.font.size = error.bitmap.font.size - 3
    continue.bitmap.draw_text(0,384,544,32,"Press Enter to exit",1)
    add = Math::PI/80; max = 2*Math::PI; angle = 0
    loop do
      Graphics.update; Input.update
      angle += add; angle %= max
      continue.opacity = 185 + 70* Math.cos(angle)
      break if Input.trigger?(Input::C)
    end
    error.bitmap.dispose; continue.bitmap.dispose
    error.bitmap = nil; continue.bitmap = nil
    error.dispose; continue.dispose
    error = nil; continue = nil
    exit
  end
end

$khas_awesome << ["Sapphire Action System",4.4]

#-------------------------------------------------------------------------------
# * Sapphire Enemy
#-------------------------------------------------------------------------------

class Sapphire_Enemy
  attr_accessor :event
  attr_accessor :id
  attr_accessor :char_file
  attr_accessor :char_index
  attr_accessor :animation
  attr_accessor :skills
  attr_accessor :object
  attr_accessor :view
  attr_accessor :recover
  attr_accessor :step_anime
  attr_accessor :nature
  attr_accessor :auto_attack
  attr_accessor :attack
  attr_accessor :defence
  attr_accessor :exp
  attr_accessor :hp
  attr_accessor :atk_invincible
  attr_accessor :skl_invincible
  attr_accessor :die_switch
  attr_accessor :die_variable
  attr_accessor :die_localsw
  attr_accessor :die_erase
  attr_accessor :magic
  attr_accessor :mdefence
  attr_accessor :static
  def initialize(event,id)
    @event = event
    @id = id
    @game_enemy = Game_Enemy.new(0,@id)
    setup_enemy
    setup_skills
    setup_nature
    @attack = @game_enemy.atk
    @defence = @game_enemy.def
    @magic = @game_enemy.mat
    @mdefence = @game_enemy.mdf
    @exp = @game_enemy.exp
    @hp = @game_enemy.mhp
    @atk_invincible = false
    @skl_invincible = false
    @die_switch = nil
    @die_variable = nil
    @die_localsw = nil
    @die_erase = false
  end
  def setup_nature
    @nature = 0 if @skills.empty?
  end
  def setup_enemy
    @animation = @game_enemy.enemy.animation
    @char_file = @game_enemy.enemy.char_file
    @char_index = @game_enemy.enemy.char_index
    @object = @game_enemy.enemy.object?
    @view = @game_enemy.enemy.view
    @recover = @game_enemy.enemy.recover
    @step_anime = @game_enemy.enemy.step_anime?
    @nature = @game_enemy.enemy.nature
    @auto_attack = @game_enemy.enemy.auto_attack
    @static = @game_enemy.enemy.static
  end
  def setup_skills
    ids = @game_enemy.enemy.skills
    @skills = []
    ids.each { |i|;
    skill = $data_skills[i];
    skills << [skill,skill.particle] unless skill.particle.nil?}
  end
end

#-------------------------------------------------------------------------------
# * Sapphire Particle
#-------------------------------------------------------------------------------

class Sapphire_Particle < Sprite
  attr_accessor :done
  def initialize(key,char)
    super(nil)
    @key = key
    self.bitmap = Sapphire_Bitcore[@key]
    self.ox = self.bitmap.width/2
    self.oy = self.bitmap.height/2
    self.z = 200
    self.angle = rand(360)
    @add = rand(10)
    @done = false
    @rx = char.real_x
    @ry = char.real_y
    self.blend_type = char.blend
  end
  def update
    self.x = $game_map.adjust_unlx(@rx) * 32 + 16
    self.y = $game_map.adjust_unly(@ry) * 32 + 16
    self.angle += @add
    self.opacity <= 0 ? dispose : self.opacity -= 30
  end
  def release
    return Virtual_Particle.new(self.x,self.y,@rx,@ry,@key,self.z,self.angle,@add,self.blend_type,self.opacity)
  end
  def dispose
    self.bitmap = nil
    super
    @done = true
  end
end

#-------------------------------------------------------------------------------
# * Sapphire Restored Particle
#-------------------------------------------------------------------------------

class Sapphire_Restored_Particle < Sprite
  attr_accessor :done
  def initialize(vp)
    super(nil)
    @key = vp.key
    self.bitmap = Sapphire_Bitcore[@key]
    self.ox = self.bitmap.width/2
    self.oy = self.bitmap.height/2
    self.z = vp.z
    self.angle = vp.angle
    @add = vp.add
    @done = false
    @rx = vp.rx
    @ry = vp.ry
    self.blend_type = vp.blend
    self.opacity = vp.opacity
  end
  def update
    self.x = $game_map.adjust_unlx(@rx) * 32 + 16
    self.y = $game_map.adjust_unly(@ry) * 32 + 16
    self.angle += @add
    self.opacity <= 0 ? dispose : self.opacity -= 30
  end
  def release
    return Virtual_Particle.new(self.x,self.y,@rx,@ry,@key,self.z,self.angle,@add,self.blend_type,self.opacity)
  end
  def dispose
    self.bitmap = nil
    super
    @done = true
  end
end

#-------------------------------------------------------------------------------
# * Virtual Particle
#-------------------------------------------------------------------------------

class Virtual_Particle
  attr_reader :x
  attr_reader :y
  attr_reader :rx
  attr_reader :ry
  attr_reader :key
  attr_reader :z
  attr_reader :angle
  attr_reader :add
  attr_reader :blend
  attr_reader :opacity
  def initialize(x,y,rx,ry,key,z,angle,add,blend,opacity)
    @x = x
    @y = y
    @rx = rx
    @ry = ry
    @key = key
    @z = z
    @angle = angle
    @add = add
    @blend = blend
    @opacity = opacity
  end
end

#-------------------------------------------------------------------------------
# * Sapphire Skill
#-------------------------------------------------------------------------------

class Sapphire_Skill
  include Pixel_Core
  attr_accessor :px
  attr_accessor :py
  attr_accessor :cx
  attr_accessor :cy
  attr_reader :x
  attr_reader :y
  attr_reader :real_x
  attr_reader :real_y
  attr_reader :move_speed
  attr_reader :move_frequency
  attr_reader :direction
  attr_reader :priority_type
  attr_reader :skill
  attr_reader :done
  attr_reader :blend
  def initialize(char)
    @char = char
    if @char.is_a?(Game_Event)
      skills = char.enemy.skills
      select = skills[rand(skills.size)]
      @skill = select[0]
      @bitmap = select[1]
      @power = @char.enemy.magic
      @cast_by_enemy = true
    else
      @skill = $game_player.current_skill[0]
      @bitmap = $game_player.current_skill[1]
      @power = $game_party.members[0].mat
      @cast_by_enemy = false
    end
    @real_x = @char.x
    @real_y = @char.y
    @x = @char.x.to_f
    @y = @char.y.to_f
    @px = @char.px
    @py = @char.py
    @move_speed = @skill.speed
    @move_frequency = 6
    @direction = @char.direction
    @cx = 3
    @cy = 3
    @done = false
    @last_move = false
    @remaining = 0
    @blend = @skill.blend
    @water_remaining = 0
    RPG::SE.new(@skill.cast_se,Sapphire_Core::Skill_Volume).play unless @skill.cast_se.nil?
  end
  def perform_damage(char)
    if @cast_by_enemy
      char.animation_id = @skill.animation_id
      char.set_direction(10-@direction)
      3.times do; char.move_backward; end
      char.do_step
      damage = @power + @skill.power
      damage += rand(damage*Sapphire_Core::Damage_Random).to_i
      $game_player.skill_damage_hero(damage)
    else
      char.animation_id = @skill.animation_id
      unless char.enemy.object
        char.set_direction(10-@direction)
        3.times do; char.move_backward; end
        char.do_step
      end
      damage = @power + @skill.power
      damage += rand(damage*Sapphire_Core::Damage_Random).to_i
      char.skill_damage_enemy(damage,true) unless char.enemy.skl_invincible
    end
  end
  def moving?
    @real_x != @x || @real_y != @y
  end
  def distance_per_frame
    2 ** @move_speed / 256.0
  end
  def screen_x
    $game_map.adjust_unlx(@real_x) * 32 + 16
  end
  def screen_y
    $game_map.adjust_unly(@real_y) * 32 + 16
  end
  def update
    cast_particle
    move unless moving?
    return update_move if moving?
  end
  def move
    @last_move ? move_last : move_pixel
  end
  def move_last
    if @remaining > 0
      @px += Tile_Range[@direction][0]
      @py += Tile_Range[@direction][1]
      @real_x = @x
      @real_y = @y
      @x += Pixel_Range[@direction][0]
      @y += Pixel_Range[@direction][1]
      @remaining -= 1
    else
      destroy
    end
  end
  def destroy
    @done = true
  end
  def cast_particle
    $game_map.particles << Sapphire_Particle.new(@bitmap,self)
  end
  def update_move
    @real_x = [@real_x - distance_per_frame, @x].max if @x < @real_x
    @real_x = [@real_x + distance_per_frame, @x].min if @x > @real_x
    @real_y = [@real_y - distance_per_frame, @y].max if @y < @real_y
    @real_y = [@real_y + distance_per_frame, @y].min if @y > @real_y
  end
  def pixel_range?(px,py)
    return (@px - px).abs <= @cx && (@py - py).abs <= @cy
  end
  def pixel_passable?(px,py,d)
    nx = px+Tile_Range[d][0]
    ny = py+Tile_Range[d][1]
    return false unless $game_map.pixel_valid?(nx,ny)
    return false if $game_map.pixel_table[px+Tile_Range[d][0],py+Tile_Range[d][1],1] == 0
    return false if collision?(nx,ny)
    return true
  end
  def collision?(px,py)
    if @cast_by_enemy
      for event in $game_map.events.values
        if (event.px - px).abs < event.cx && (event.py - py).abs < event.cy
          next if event.through || event == @char
          return true if event.priority_type == 1
        end
      end
      return ($game_player.px - px).abs <= @cx && ($game_player.py - py).abs <= @cy
    else
      for event in $game_map.events.values
        if (event.px - px).abs < event.cx && (event.py - py).abs < event.cy
          next if event.through
          return true if event.priority_type == 1
        end
      end
      return false
    end
  end
  def move_pixel
    if pixel_passable?(@px,@py,@direction)
      @px += Tile_Range[@direction][0]
      @py += Tile_Range[@direction][1]
      @real_x = @x
      @real_y = @y
      @x += Pixel_Range[@direction][0]
      @y += Pixel_Range[@direction][1]
    else
      front_pixel_touch?(@px + Tile_Range[@direction][0],@py + Tile_Range[@direction][1])
      @last_move = true
      @remaining = 3
    end
  end
  def front_pixel_touch?(px,py)
    if @cast_by_enemy
      perform_damage($game_player) if ($game_player.px - px).abs <= @cx && ($game_player.py - py).abs <= @cy
    else
      for event in $game_map.enemies
        if (event.px - px).abs < event.cx && (event.py - py).abs < event.cy
          next if event.enemy.static
          perform_damage(event)
        end
      end
    end
  end
end

#-------------------------------------------------------------------------------
# * Sapphire HUD
#-------------------------------------------------------------------------------

class Sapphire_Hud
  def refresh_bars(arg=nil)
  end
  def refresh_base
  end
  def hide(arg=nil)
  end
  def show(arg=nil)
  end
end

#-------------------------------------------------------------------------------
# * RGSS3 Object
#-------------------------------------------------------------------------------

class Object
  def check(string)
    self.each_line { |i| return true if i =~ /#{string}/i }
    return false
  end
  def get(string,default=nil)    
    self.each_line { |i| return i.gsub("#{string} = ", "").chomp if i =~ /#{string} = /i }
    return default
  end
end

#-------------------------------------------------------------------------------
# * Cache
#-------------------------------------------------------------------------------

module Cache
  def self.particle(filename)
    load_bitmap("Graphics/Particles/", filename)
  end
end

#-------------------------------------------------------------------------------
# * RPG::Enemy
#-------------------------------------------------------------------------------

class RPG::Enemy < RPG::BaseItem
  def skills
    value = self.note.get("Skills","")
    return eval("[#{value}]")
  end
  def object?
    self.note.check("Object")
  end
  def view
    self.note.get("View", Sapphire_Core::Enemy_View).to_i
  end
  def recover
    self.note.get("Recover", Sapphire_Core::Enemy_Recover).to_i
  end
  def step_anime?
    self.note.check("StepAnime")
  end
  def nature
    self.note.get("Nature", Sapphire_Core::Enemy_Nature).to_i
  end
  def char_file
    self.note.get("Char",nil)
  end
  def char_index
    self.note.get("Char_index",0).to_i
  end
  def animation
    self.note.get("Animation",0).to_i
  end
  def auto_attack
    self.note.check("Auto_Attack")
  end
  def static
    self.note.check("Static")
  end
end

#-------------------------------------------------------------------------------
# * RPG::Skill
#-------------------------------------------------------------------------------

class RPG::Skill < RPG::UsableItem
  attr_reader :recover
  def particle
    self.note.get("Particle", nil)
  end
  def speed
    self.note.get("Speed", Sapphire_Core::Default_Skill_Speed).to_i
  end
  def blend
    self.note.get("Blend", Sapphire_Core::Default_Particle_Blend).to_i
  end
  def set_recover
    @recover = self.note.get("Recover", Sapphire_Core::Default_Skill_Recover).to_i
  end
  def power
    self.note.get("Power", 0).to_i
  end
  def cast_se
    self.note.get("Sound", nil)
  end
end

#-------------------------------------------------------------------------------
# * Scene Map
#-------------------------------------------------------------------------------

class Scene_Map < Scene_Base
  attr_accessor :spriteset
end

#-------------------------------------------------------------------------------
# * Sprite Base
#-------------------------------------------------------------------------------

class Sprite_Base
  Reduce = 3
  def animation_set_sprites(frame)
    cell_data = frame.cell_data
    @ani_sprites.each_with_index do |sprite, i|
      next unless sprite
      pattern = cell_data[i, 0]
      if !pattern || pattern < 0
        sprite.visible = false
        next
      end
      sprite.bitmap = pattern < 100 ? @ani_bitmap1 : @ani_bitmap2
      sprite.visible = true
      sprite.src_rect.set(pattern % 5 * 192,
        pattern % 100 / 5 * 192, 192, 192)
      if @ani_mirror
        sprite.x = @ani_ox - cell_data[i, 1] / Reduce
        sprite.y = @ani_oy + cell_data[i, 2] / Reduce
        sprite.angle = (360 - cell_data[i, 4])
        sprite.mirror = (cell_data[i, 5] == 0)
      else
        sprite.x = @ani_ox + cell_data[i, 1] / Reduce
        sprite.y = @ani_oy + cell_data[i, 2] / Reduce
        sprite.angle = cell_data[i, 4]
        sprite.mirror = (cell_data[i, 5] == 1)
      end
      sprite.z = self.z + 300 + i
      sprite.ox = 96
      sprite.oy = 96
      sprite.zoom_x = cell_data[i, 3] / (100.0 * Reduce)
      sprite.zoom_y = cell_data[i, 3] / (100.0 * Reduce)
      sprite.opacity = cell_data[i, 6] * self.opacity / 255.0
      sprite.blend_type = cell_data[i, 7]
    end
  end
end

#-------------------------------------------------------------------------------
# * Spriteset Map
#-------------------------------------------------------------------------------

class Spriteset_Map
  alias sas_update update
  alias sas_initialize initialize
  alias sas_dispose dispose
  def initialize
    @trash = []
    $game_map.show_particles
    $game_map.show_damage_sprites
    $game_map.sas_hud.show
    sas_initialize
    @weapon_graphic = Sprite.new(@viewport1)
    @weapon_graphic.ox = 22
    @weapon_graphic.oy = 22
    @attacking = false
    @attack_timer = 0
    @angles = {2=>[80,110,140,170],4=>[340,10,40,70],6=>[290,260,230,200],8=>[290,320,350,20]}
    @correction = {2=>[-8,-10],4=>[0,-10],6=>[0,-4],8=>[4,-10]}
    @z_values = {2=>120,4=>50,6=>120,8=>50}
    refresh_weapon
  end
  def refresh_weapon
    @weapon_bitmap.dispose unless @weapon_bitmap.nil?
    @weapon_bitmap = nil
    return if $game_party.members.empty?
    index = ($game_party.members[0].weapons[0].icon_index rescue nil)
    unless index == nil
      temp = Cache.system("Iconset")
      @weapon_bitmap = Bitmap.new(24,24)
      @weapon_bitmap.blt(0,0,temp,Rect.new(index%16*24,index/16*24,24,24))
      temp.dispose
      temp = nil
    end
  end
  def dispose
    sas_dispose
    $game_map.sas_hud.hide
    $game_map.hide_particles
    $game_map.hide_damage_sprites
    @weapon_graphic.bitmap = nil
    unless @weapon_bitmap.nil?
      @weapon_bitmap.dispose
      @weapon_bitmap = nil
    end
    @weapon_graphic.dispose
    @weapon_graphic = nil
  end
  def update
    sas_update
    update_particles
    update_damage_sprites
    update_weapon_graphic if @attacking
  end
  def update_damage_sprites
  end
  def update_particles
    $game_map.particles.each { |particle| particle.update; @trash << particle if particle.done }
    @trash.each { |item| $game_map.particles.delete(item) }
    @trash.clear
  end
  def update_weapon_graphic
    @weapon_graphic.x = $game_player.screen_x + @correction[$game_player.direction][0]
    @weapon_graphic.y = $game_player.screen_y + @correction[$game_player.direction][1]
    case @attack_timer
    when 12
      @weapon_graphic.angle = @angles[$game_player.direction][0]
      @weapon_graphic.z = @z_values[$game_player.direction]
    when 9
      @weapon_graphic.angle = @angles[$game_player.direction][1]
      @weapon_graphic.z = @z_values[$game_player.direction]
    when 6
      @weapon_graphic.angle = @angles[$game_player.direction][2]
      @weapon_graphic.z = @z_values[$game_player.direction]
    when 3
      @weapon_graphic.angle = @angles[$game_player.direction][3]
      @weapon_graphic.z = @z_values[$game_player.direction]
    when 0
      @attacking = false
      @weapon_graphic.bitmap = nil
    end
    @weapon_graphic.update
    @attack_timer -= 1
  end
  def weapon_animation
    return if @weapon_bitmap.nil?
    @weapon_graphic.bitmap = @weapon_bitmap
    @attacking = true
    @attack_timer = 12
  end
end

#-------------------------------------------------------------------------------
# * Game Map
#-------------------------------------------------------------------------------

class Game_Map
  include Pixel_Core
  attr_accessor :enemies
  attr_reader :sas_active
  attr_accessor :particles
  attr_accessor :skills
  attr_accessor :sas_hud
  attr_accessor :damage_sprites
  attr_reader :pixel_table
  alias kp_referesh_vehicles referesh_vehicles
  alias sas_update update
  alias sas_setup_events setup_events
  alias sas_initialize initialize
  def initialize
    sas_initialize
    @sas_hud = Sapphire_Hud.new
    @trash = []
  end
  def damage(target,value)
  end
  def level_up
  end
  def hide_damage_sprites
  end
  def show_damage_sprites
  end
  def setup_events
    @enemies = []
    sas_setup_events
  end
  def update(arg=false)
    sas_update(arg)
    update_skills
    update_action_system if @sas_active && arg
  end
  def update_action_system
    if Input.trigger?(Input::X)
      $game_player.attack
    elsif Input.trigger?(Input::Y)
      $game_player.cast_skill
    elsif Input.trigger?(Input::Z)
      $game_player.next_skill
    end
  end
  def start_sas
    @sas_active = true
  end
  def pause_sas
    @sas_active = false
  end
  def hide_particles
    virtual_particles = []
    @particles.each { |particle| virtual_particles << particle.release; particle.dispose }
    @particles = virtual_particles
  end
  def show_particles
    virtual_particles = @particles
    @particles = []
    virtual_particles.each { |vp| @particles << Sapphire_Restored_Particle.new(vp)}
    virtual_particles.clear
  end
  def delete_particles
    if @particles.nil?
      @particles = []
    else
      @particles.each { |particle| particle.dispose }
      @particles.clear
    end
  end
  def delete_skills
    if @skills.nil?
      @skills = []
    else
      @skills.each { |skill| skill.destroy }
      @skills.clear
    end
  end
  def delete_damage_sprites
  end
  def adjust_unlx(x)
    return x - @display_x
  end
  def adjust_unly(y)
    return y - @display_y
  end
  def update_skills
    @skills.each { |skill| skill.update; @trash << skill if skill.done }
    @trash.each { |item| @skills.delete(item) }
    @trash.clear
  end
  def pixel_valid?(x, y)
    x >= 0 && x <= @pixel_wm && y >= 0 && y <= @pixel_hm
  end
  def referesh_vehicles
    setup_table
    delete_particles
    delete_skills
    delete_damage_sprites
    kp_referesh_vehicles
  end
  def setup_table
    @pixel_table = Table.new(width*Pixel, height*Pixel,6)
    for x in 0...(width*Pixel)
      for y in 0...(height*Pixel)
        @pixel_table[x,y,0] = table_player_collision(x*Tile,y*Tile)
        @pixel_table[x,y,1] = table_skill_collision(x*Tile,y*Tile)
        @pixel_table[x,y,3] = table_ladder(x*Tile,y*Tile)
        @pixel_table[x,y,4] = table_bush(x*Tile+Bush_Axis[0],y*Tile+Bush_Axis[1])
        @pixel_table[x,y,5] = table_counter(x*Tile+Counter_Axis[0],y*Tile+Counter_Axis[1])
      end
    end
    @pixel_wm = (width-1)*Pixel
    @pixel_hm = (height-1)*Pixel
  end
  def table_player_collision(x,y)
    return 0 unless table_pp((x+Body_Axis[0]).to_i,(y+Body_Axis[1]).to_i)
    return 0 unless table_pp((x+Body_Axis[2]).to_i,(y+Body_Axis[1]).to_i)
    return 0 unless table_pp((x+Body_Axis[0]).to_i,(y+Body_Axis[3]).to_i)
    return 0 unless table_pp((x+Body_Axis[2]).to_i,(y+Body_Axis[3]).to_i)
    return 1
  end
  def table_skill_collision(x,y)
    return 0 unless table_ps((x+Body_Axis[0]).to_i,(y+Body_Axis[1]).to_i)
    return 0 unless table_ps((x+Body_Axis[2]).to_i,(y+Body_Axis[1]).to_i)
    return 0 unless table_ps((x+Body_Axis[0]).to_i,(y+Body_Axis[3]).to_i)
    return 0 unless table_ps((x+Body_Axis[2]).to_i,(y+Body_Axis[3]).to_i)
    return 1
  end
  def refresh_table(start_x,start_y,end_x,end_y)
    for x in (start_x*Pixel)..(end_x*Pixel)
      for y in (start_y*Pixel)..(end_y*Pixel)
        @pixel_table[x,y,0] = table_pcrf(x*Tile,y*Tile)
        @pixel_table[x,y,1] = table_scrf(x*Tile,y*Tile)
      end
    end
  end
  def refresh_table_px(start_px,start_py,end_px,end_py)
    for x in start_px..end_px
      for y in start_py..end_py
        @pixel_table[x,y,0] = table_pcrf(x*Tile,y*Tile)
        @pixel_table[x,y,1] = table_scrf(x*Tile,y*Tile)
      end
    end
  end
  def table_pcrf(x,y)
    return 0 unless table_pprf((x+Body_Axis[0]).to_i,(y+Body_Axis[1]).to_i)
    return 0 unless table_pprf((x+Body_Axis[2]).to_i,(y+Body_Axis[1]).to_i)
    return 0 unless table_pprf((x+Body_Axis[0]).to_i,(y+Body_Axis[3]).to_i)
    return 0 unless table_pprf((x+Body_Axis[2]).to_i,(y+Body_Axis[3]).to_i)
    return 1
  end
  def table_scrf(x,y)
    return 0 unless table_psrf((x+Body_Axis[0]).to_i,(y+Body_Axis[1]).to_i)
    return 0 unless table_psrf((x+Body_Axis[2]).to_i,(y+Body_Axis[1]).to_i)
    return 0 unless table_psrf((x+Body_Axis[0]).to_i,(y+Body_Axis[3]).to_i)
    return 0 unless table_psrf((x+Body_Axis[2]).to_i,(y+Body_Axis[3]).to_i)
    return 1
  end
  def table_p(x,y,bit)
    layered_tiles(x,y).each do |tile_id|
      flag = tileset.flags[tile_id]
      next if flag & 0x10 != 0
      return true  if flag & bit == 0
      return false if flag & bit == bit
    end
    return false
  end
  def table_pp(x,y)
    layered_tiles(x,y).each do |tile_id|
      flag = tileset.flags[tile_id]
      next if flag & 0x10 != 0
      return true if flag & 0x0f == 0
      return false if flag & 0x0f == 0x0f
    end
    return false
  end
  def table_ps(x,y)
    layered_tiles(x,y).each do |tile_id|
      flag = tileset.flags[tile_id]
      next if flag & 0x10 != 0
      return true if flag & 0x0400 == 0
      return true if flag & 0x0f == 0
      return false if flag & 0x0f == 0x0f
    end
    return false
  end
  def table_pprf(x,y)
    all_tiles(x, y).each do |tile_id|
      flag = tileset.flags[tile_id]
      next if flag & 0x10 != 0
      return true if flag & 0x0f == 0
      return false if flag & 0x0f == 0x0f
    end
    return false
  end
  def table_psrf(x,y)
    all_tiles(x,y).each do |tile_id|
      flag = tileset.flags[tile_id]
      next if flag & 0x10 != 0
      return true if flag & 0x0400 == 0
      return true if flag & 0x0f == 0
      return false if flag & 0x0f == 0x0f
    end
    return false
  end
  def table_bush(x,y)
    return layered_tiles_flag?(x.to_i, y.to_i, 0x40) ? 1 : 0
  end
  def table_ladder(x,y)
    return 1 if layered_tiles_flag?(x.to_i,(y+Ladder_Axis[1]).to_i, 0x20)
    return 1 if layered_tiles_flag?((x+Ladder_Axis[0]).to_i, (y+Ladder_Axis[1]).to_i, 0x20)
    return 0
  end
  def table_counter(x,y)
    return 1 if layered_tiles_flag?(x.to_i,y.to_i, 0x80)
    return 1 if layered_tiles_flag?((x+Counter_Axis[2]).to_i,y.to_i, 0x80)
    return 1 if layered_tiles_flag?(x.to_i,(y+Counter_Axis[3]).to_i, 0x80)
    return 1 if layered_tiles_flag?((x+Counter_Axis[2]).to_i,(y+Counter_Axis[3]).to_i, 0x80)
    return 0
  end
end

if Pixel_Core::Auto_Refresh_Tile_Events
  class Game_Map
    def refresh_tile_events
      @tile_events = @events.values.select {|event| event.tile? }
      @tile_events.each { |event| refresh_table_px(event.px-TileEvent_Range,event.py-TileEvent_Range,event.px+TileEvent_Range,event.py+TileEvent_Range)}
    end
  end
end

#-------------------------------------------------------------------------------
# * Game CharacterBase
#-------------------------------------------------------------------------------

class Game_CharacterBase
  include Pixel_Core
  attr_accessor :px
  attr_accessor :py
  attr_accessor :cx
  attr_accessor :cy
  alias kp_moveto moveto
  alias kp_move_straight move_straight
  alias kp_move_diagonal move_diagonal
  alias kp_bush? bush?
  alias kp_ladder? ladder?
  alias kp_terrain_tag terrain_tag
  alias kp_region_id region_id
  alias sas_update update
  alias sas_public_members init_public_members
  alias sas_straighten straighten
  def pixel_range?(px,py)
    return (@px - px).abs <= @cx && (@py - py).abs <= @cy
  end
  def update
    sas_update
    update_step_action if @step_action
  end
  def straighten
    sas_straighten
    @step_action = false
    @step_timer = 0
  end
  def update_step_action
    case @step_timer
    when 12; @pattern = 0
    when 8; @pattern = 1
    when 4; @pattern = 2
    when 0
      @step_action = false
      @pattern = 1
      return
    end
    @step_timer -= 1
  end
  def do_step
    @step_action = true
    @step_timer = 12
  end
  def init_public_members
    sas_public_members
    @x = @x.to_f
    @y = @y.to_f
    @px = (@x*Pixel).to_i
    @py = (@y*Pixel).to_i
    @cx = Default_Collision_X
    @cy = Default_Collision_Y
    @step_action = false
    @step_timer = 0
  end
  def moveto(x,y)
    kp_moveto(x,y)
    @x = @x.to_f
    @y = @y.to_f
    @px = (@x*Pixel).to_i
    @py = (@y*Pixel).to_i
  end
  def pixel_passable?(px,py,d)
    nx = px+Tile_Range[d][0]
    ny = py+Tile_Range[d][1]
    return false unless $game_map.pixel_valid?(nx,ny)
    return true if @through || debug_through?
    return false if $game_map.pixel_table[nx,ny,0] == 0
    return false if collision?(nx,ny)
    return true
  end
  def collision?(px,py)
    for event in $game_map.events.values
      if (event.px - px).abs <= event.cx && (event.py - py).abs <= event.cy
        next if event.through || event == self
        return true if event.priority_type == 1
      end
    end
    if @priority_type == 1
      return true if ($game_player.px - px).abs <= @cx && ($game_player.py - py).abs <= @cy
    end
    return false
  end
  def move_straight(d,turn_ok = true)
    move_pixel(d,turn_ok)
  end
  def move_diagonal(horz, vert)
    move_dpixel(horz,vert)
  end
  def move_pixel(d,t)
    @move_succeed = pixel_passable?(@px,@py,d)
    if @move_succeed
      set_direction(d)
      @px += Tile_Range[d][0]
      @py += Tile_Range[d][1]
      @real_x = @x
      @real_y = @y
      @x += Pixel_Range[d][0]
      @y += Pixel_Range[d][1]
      increase_steps
    elsif t
      set_direction(d)
      front_pixel_touch?(@px + Tile_Range[d][0],@py + Tile_Range[d][1])
    end
  end
  def move_dpixel(h,v)
    @move_succeed = false
    if pixel_passable?(@px,@py,v)
      @move_succeed = true
      @real_x = @x
      @real_y = @y
      set_direction(v)
      @px += Tile_Range[v][0]
      @py += Tile_Range[v][1]
      @x += Pixel_Range[v][0]
      @y += Pixel_Range[v][1]
      increase_steps
    else
      set_direction(v)
      front_pixel_touch?(@px + Tile_Range[v][0],@py + Tile_Range[v][1])
    end
    if pixel_passable?(@px,@py,h)
      unless @move_succeed 
        @real_x = @x
        @real_y = @y
        @move_succeed = true
      end
      set_direction(h)
      @px += Tile_Range[h][0]
      @py += Tile_Range[h][1]
      @x += Pixel_Range[h][0]
      @y += Pixel_Range[h][1]
      increase_steps
    else
      set_direction(h)
      front_pixel_touch?(@px + Tile_Range[h][0],@py + Tile_Range[h][1])
    end
  end
  def bush?
    return $game_map.pixel_table[@px, @py, 4] == 1
  end
  def ladder?
    return $game_map.pixel_table[@px, @py, 3] == 1
  end
  def terrain_tag
    rx = ((@px % Pixel) > 1 ? @x.to_i + 1 : @x.to_i)
    ry = ((@py % Pixel) > 1 ? @y.to_i + 1 : @y.to_i)
    return $game_map.terrain_tag(rx,ry)
  end
  def region_id
    rx = ((@px % Pixel) > 1 ? @x.to_i + 1 : @x.to_i)
    ry = ((@py % Pixel) > 1 ? @y.to_i + 1 : @y.to_i)
    return $game_map.region_id(rx, ry)
  end
  def front_pixel_touch?(x,y)
  end
end

#-------------------------------------------------------------------------------
# * Game FakeFollowers
#-------------------------------------------------------------------------------

class Game_FakeFollowers
  attr_accessor :visible
  def initialize
    @visible = true
  end
  def refresh
  end
  def update
  end
  def gathering?
    return false
  end
  def synchronize(x,y,d)
  end
  def collide?(x,y)
    return false
  end
  def gather
  end
  def gather?
    return true
  end
  def reverse_each
    return []
  end
  def each
    return []
  end
end

#-------------------------------------------------------------------------------
# * Game Character
#-------------------------------------------------------------------------------

class Game_Character < Game_CharacterBase
  attr_accessor :pattern 
  alias kp_force_move_route force_move_route
  alias kp_move_toward_character move_toward_character
  alias kp_move_away_from_character move_away_from_character
  alias kp_jump jump
  def force_move_route(route)
    kp_force_move_route(route.clone)
    multiply_commands
  end
  def multiply_commands
    return unless Multiply_Commands
    return if @move_route.list.empty?
    new_route = []
    for cmd in @move_route.list
      if Commands.include?(cmd.code)
        Pixel.times do
          new_route << cmd
        end
      else
        new_route << cmd
      end
    end
    @move_route.list = new_route
  end
  def move_toward_character(character)
    dx = @px - character.px
    dy = @py - character.py
    if dx.abs < character.cx
      unless dy.abs < character.cy
        move_pixel(dy < 0 ? 2 : 8,true) 
        unless @move_succeed
          return if dx.abs - Chase_Axis[@direction][0] <= @cx && dy.abs - Chase_Axis[@direction][1] <= @cy
          move_dpixel(dx < 0 ? 6 : 4, dy < 0 ? 2 : 8)
        end
      end
    else
      if dy.abs < character.cy
        move_pixel(dx < 0 ? 6 : 4,true)
        unless @move_succeed
          return if dx.abs - Chase_Axis[@direction][0] <= @cx && dy.abs - Chase_Axis[@direction][1] <= @cy
          move_dpixel(dx < 0 ? 6 : 4, dy < 0 ? 2 : 8)
        end
      else
        move_dpixel(dx < 0 ? 6 : 4, dy < 0 ? 2 : 8)
      end
    end
  end
  def move_away_from_character(character)
    dx = @px - character.px
    dy = @py - character.py
    if dx == 0
      move_pixel(dy > 0 ? 2 : 8,true)
    else
      if dy == 0 
        move_pixel(dx > 0 ? 6 : 4,true)
      else
        move_dpixel(dx > 0 ? 6 : 4, dy > 0 ? 2 : 8)
      end
    end
  end
  def jump(xp,yp)
    kp_jump(xp,yp)
    @px = @x*Pixel
    @py = @y*Pixel
  end
end

#-------------------------------------------------------------------------------
# * Game Player
#-------------------------------------------------------------------------------

class Game_Player < Game_Character
  attr_accessor :recover
  attr_accessor :current_skill
  alias sas_initialize initialize
  alias sas_player_update update
  def update
    sas_player_update
    @recover -= 1 if @recover > 0
  end
  def straighten
    super
    refresh_weapon_stats
    @recover = 0
  end
  def initialize
    sas_initialize
    @followers = Game_FakeFollowers.new
    @current_skill = [nil,nil]
  end
  def update_vehicle
  end
  def cast_skill
    return if @current_skill[0].nil? || @recover > 0
    return if $game_party.members[0].mp < @current_skill[0].mp_cost
    $game_map.skills << Sapphire_Skill.new(self)
    $game_party.members[0].mp -= @current_skill[0].mp_cost
    $game_map.sas_hud.refresh_bars
    @recover = @current_skill[0].recover
  end
  def next_skill
    unless @current_skill[1].nil?
      @current_skill[1] = nil
    end
    skills = $game_party.members[0].skills
    if skills.empty?
      @current_skill = [nil,nil] 
    else
      ns = 0
      unless @current_skill[0].nil?
        max = skills.size-1
        for id in 0..max
          ns = (id == max ? 0 : id + 1) if skills[id] == @current_skill[0]
        end
      end
      skills[ns].set_recover
      @current_skill = [skills[ns],skills[ns].particle]
      $game_map.sas_hud.refresh_base
    end
  end
  def damage_hero(value)
    actor = $game_party.members[0]
    value -= actor.def
    value = 0 if value < 0
    $game_map.show_text(self,value)
    if actor.hp <= value
      actor.hp = 1
      $game_map.sas_hud.refresh_bars(0)
      kill_player
    else
      actor.hp -= value
      $game_map.sas_hud.refresh_bars
    end
  end
  def skill_damage_hero(value)
    actor = $game_party.members[0]
    value -= actor.mdf
    value = 0 if value < 0
    $game_map.show_text(self,value)
    if actor.hp <= value
      actor.hp = 1
      $game_map.sas_hud.refresh_bars(0)
      kill_player
    else
      actor.hp -= value
      $game_map.sas_hud.refresh_bars
    end
  end
  def kill_player
    $game_map.pause_sas
    $game_switches[Sapphire_Core::Kill_Switch] = true
    $game_map.need_refresh = true
  end
  def attack
    return if @recover > 0 || $game_map.interpreter.running?
    can_move = true
    @recover = @max_recover
    SceneManager.scene.spriteset.weapon_animation if Sapphire_Core::Enable_Weapon_Graphics
    play_voice if Sapphire_Core::Enable_Voice
    tx = @px + Sapphire_Core::Weapon_Range[@direction][0]
    ty = @py + Sapphire_Core::Weapon_Range[@direction][1]
    for char in $game_map.enemies
      if char.pixel_range?(tx,ty)
        next if char.enemy.static
        char.animation_id = @weapon_animation
        unless char.enemy.object
          char.turn_toward_character(self)
          3.times do; char.move_backward; end
          char.do_step
        else
          can_move = false 
        end
        damage = $game_party.members[0].atk
        damage += rand(damage*Sapphire_Core::Damage_Random).to_i
        char.damage_enemy(damage,true) unless char.enemy.atk_invincible
      end
    end 
    return unless can_move
    do_step
    move_forward
  end
  def get_weapon_recover(actor)
    for feature in actor.weapons[0].features
      return feature.value if feature.code == 33
    end
    return Sapphire_Core::Default_Recover
  end
  def refresh_weapon_stats
    hero = $game_party.members[0]
    if hero.weapons[0].nil?
      @max_recover = Sapphire_Core::Default_Recover
      @weapon_animation = Sapphire_Core::Default_Animation
    else
      @max_recover = get_weapon_recover(hero)
      @weapon_animation = hero.weapons[0].animation_id
    end
  end
  def play_voice
    RPG::SE.new(Sapphire_Core::Voice_Files[rand(Sapphire_Core::Voice_Files.size)],Sapphire_Core::Voice_Volume).play 
  end
  def encounter_progress_value
    return 1
  end
  def get_on_off_vehicle
    return false
  end
  def check_event_trigger_here(triggers)
    for event in $game_map.events.values
      if (event.px - @px).abs <= event.cx && (event.py - @py).abs <= event.cy
        event.start if triggers.include?(event.trigger) && event.priority_type != 1
      end
    end
  end
  def check_event_trigger_there(triggers)
    fx = @px+Trigger_Range[@direction][0]
    fy = @py+Trigger_Range[@direction][1]
    for event in $game_map.events.values
      if (event.px - fx).abs <= event.cx && (event.py - fy).abs <= event.cy
        if triggers.include?(event.trigger) && event.normal_priority?
          event.start
          return
        end
      end
    end
    if $game_map.pixel_table[fx,fy,5] == 1
      fx += Counter_Range[@direction][0]
      fy += Counter_Range[@direction][1]
      for event in $game_map.events.values
        if (event.px - fx).abs <= event.cx && (event.py - fy).abs <= event.cy
          if triggers.include?(event.trigger) && event.normal_priority?
            event.start
            return
          end
        end
      end
    end
  end
  def front_pixel_touch?(px,py)
    return if $game_map.interpreter.running?
    for event in $game_map.events.values
      if (event.px - px).abs <= event.cx && (event.py - py).abs <= event.cy
        if [1,2].include?(event.trigger) && event.normal_priority?
          event.start
          result = true
        end
      end
    end
  end
  def pixel_passable?(px,py,d)
    nx = px+Tile_Range[d][0]
    ny = py+Tile_Range[d][1]
    return false unless $game_map.pixel_valid?(nx,ny)
    return true if @through || debug_through?
    return false if $game_map.pixel_table[nx,ny,0] == 0
    return false if collision?(nx,ny)
    return true
  end
  def move_by_input
    return if !movable? || $game_map.interpreter.running?
    case Input.dir8
      when 1; move_dpixel(4,2)
      when 2; move_pixel(2,true)
      when 3; move_dpixel(6,2)
      when 4; move_pixel(4,true)
      when 6; move_pixel(6,true)
      when 7; move_dpixel(4,8)
      when 8; move_pixel(8,true)
      when 9; move_dpixel(6,8)
    end
  end
  def on_damage_floor?
    return false
  end
  def collision?(px,py)
    for event in $game_map.events.values
      if (event.px - px).abs <= event.cx && (event.py - py).abs <= event.cy
        next if event.through
        return true if event.priority_type == 1
      end
    end
    return false
  end
  def move_straight(d, turn_ok = true)
    super(d, turn_ok)
  end
  def move_diagonal(horz, vert)
    super(horz, vert)
  end
end

#-------------------------------------------------------------------------------
# * Game Event
#-------------------------------------------------------------------------------

class Game_Event < Game_Character
  attr_accessor :enemy
  alias sas_setup_page setup_page
  alias sas_initialize initialize
  alias sas_event_update update
  alias kp_move_type_toward_player move_type_toward_player
  alias kp_setup_page_settings setup_page_settings
  def initialize(m,e)
    @enemy = nil
    @recover = 0
    @request_view = false
    sas_initialize(m,e)
    setup_collision
  end
  def update
    if $game_map.sas_active && @enemy != nil
      @request_view ? update_view : update_skills
      @recover -= 1 if @recover > 0
    end
    sas_event_update
  end
  def update_skills
    return if @recover > 0 || @enemy.nature == 0
    if @enemy.auto_attack
      $game_map.skills << Sapphire_Skill.new(self)
      @recover = @enemy.recover
    else
      update_cast
    end
  end
  def damage_enemy(value,by_player=false)
    value -= @enemy.defence
    value = 0 if value < 0
    @enemy.hp -= value
    $game_map.show_text(self,value) unless @enemy.object
    if @enemy.hp <= 0
      kill_enemy(by_player)
    elsif by_player && @request_view
      @balloon_id = 1 if Sapphire_Core::Enemy_Exclamation
      @move_type = 2
      @move_frequency = 6
      @request_view = false
    end
  end
  def skill_damage_enemy(value,by_player=false)
    value -= @enemy.mdefence
    value = 0 if value < 0
    @enemy.hp -= value
    $game_map.show_text(self,value) unless @enemy.object
    if @enemy.hp <= 0
      kill_enemy(by_player)
    elsif by_player && @request_view
      @balloon_id = 1 if Sapphire_Core::Enemy_Exclamation
      @move_type = 2
      @move_frequency = 6
      @request_view = false
    end
  end
  def attack
    @recover = @enemy.recover
    tx = @px + Sapphire_Core::Weapon_Range[@direction][0]
    ty = @py + Sapphire_Core::Weapon_Range[@direction][1]
    if $game_player.pixel_range?(tx,ty)
      $game_player.animation_id = @enemy.animation
      $game_player.turn_toward_character(self)
      3.times do; $game_player.move_backward; end
      $game_player.do_step
      damage = @enemy.attack
      damage += rand(damage*Sapphire_Core::Damage_Random).to_i
      $game_player.damage_hero(damage)
    end
    do_step
    move_forward
  end
  def kill_enemy(by_player)
    @direction = 2
    moveto(@x,@y)
    @request_view = false
    @step_anime = false
    @move_type = 0
    @character_name = ""
    @tile_id = 0
    @priority_type = 0
    @opacity = 255
    if by_player
      actor = $game_party.members[0]
      current_level = actor.level
      actor.change_exp(actor.exp + @enemy.exp,false)
      if current_level != actor.level
        $game_map.sas_hud.refresh_base 
        $game_map.level_up
      end
      $game_map.sas_hud.refresh_bars
    end
    run_enemy_commands
  end
  def update_view
    case @direction
    when 2
      distance = ($game_player.py - @py)
      if ($game_player.px - @px).abs <= @cx && distance <= @enemy.view && distance >= 0
        @balloon_id = 1 if Sapphire_Core::Enemy_Exclamation
        @move_type = 2
        @move_frequency = 6
        @request_view = false
      end
    when 4
      distance = (@px - $game_player.px)
      if ($game_player.py - @py).abs <= @cx && distance <= @enemy.view && distance >= 0
        @balloon_id = 1 if Sapphire_Core::Enemy_Exclamation
        @move_type = 2
        @move_frequency = 6
        @request_view = false
      end
    when 6
      distance = ($game_player.px - @px)
      if ($game_player.py - @py).abs <= @cx && distance <= @enemy.view && distance >= 0
        @balloon_id = 1 if Sapphire_Core::Enemy_Exclamation
        @move_type = 2
        @move_frequency = 6
        @request_view = false
      end
    when 8
      distance = (@py - $game_player.py)
      if ($game_player.px - @px).abs <= @cx && distance <= @enemy.view && distance >= 0
        @balloon_id = 1 if Sapphire_Core::Enemy_Exclamation
        @move_type = 2
        @move_frequency = 6
        @request_view = false
      end
    end
  end
  def update_cast
    case @direction
    when 2
      distance = ($game_player.py - @py)
      if ($game_player.px - @px).abs <= @cx && distance <= @enemy.view && distance >= Sapphire_Core::Enemy_Skill_Distance
        $game_map.skills << Sapphire_Skill.new(self)
        @recover = @enemy.recover
      end
    when 4
      distance = (@px - $game_player.px)
      if ($game_player.py - @py).abs <= @cx && distance <= @enemy.view && distance >= Sapphire_Core::Enemy_Skill_Distance
        $game_map.skills << Sapphire_Skill.new(self)
        @recover = @enemy.recover
      end
    when 6
      distance = ($game_player.px - @px)
      if ($game_player.py - @py).abs <= @cx && distance <= @enemy.view && distance >= Sapphire_Core::Enemy_Skill_Distance
        $game_map.skills << Sapphire_Skill.new(self)
        @recover = @enemy.recover
      end
    when 8
      distance = (@py - $game_player.py)
      if ($game_player.px - @px).abs <= @cx && distance <= @enemy.view && distance >= Sapphire_Core::Enemy_Skill_Distance
        $game_map.skills << Sapphire_Skill.new(self)
        @recover = @enemy.recover
      end
    end
  end
  def setup_page(np)
    sas_setup_page(np)
    setup_enemy(np.nil?)
  end
  def setup_enemy(dispose_enemy)
    unless @enemy.nil?
      $game_map.enemies.delete(self)
      @enemy = nil
    end
    unless dispose_enemy && @list.nil?
      for command in @list
        if command.code == 108 && command.parameters[0].include?("[enemy")
          command.parameters[0].scan(/\[enemy ([0.0-9.9]+)\]/)
          spawn_enemy($1.to_i)
          return
        end
      end
    end
  end
  def spawn_enemy(id)
    $game_map.enemies << self if @enemy.nil?
    @enemy = Sapphire_Enemy.new(self,id)
    @recover = 0
    @step_anime = @enemy.step_anime
    @request_view = true unless @enemy.object
    @character_name = @enemy.char_file unless @enemy.char_file.nil?
    @character_index = @enemy.char_index unless @enemy.char_file.nil?
    @priority_type = 1
    setup_parameters
  end
  def setup_parameters
    return if @list.nil?
    for value in 0...@list.size
      next if @list[value].code != 108 && @list[value].code != 408
      @enemy.atk_invincible = true if @list[value].parameters[0] == "[attack_invincible]"
      @enemy.skl_invincible = true if @list[value].parameters[0] == "[skill_invincible]"
      @enemy.die_erase = true if @list[value].parameters[0] == "[erase]"
      if @list[value].parameters[0].include?("[localsw")
        @list[value].parameters[0].scan(/\[localsw ([0.0-9.9]+)\]/)
        @enemy.die_localsw = $1.to_i
      end
      if @list[value].parameters[0].include?("[switch")
        @list[value].parameters[0].scan(/\[switch ([0.0-9.9]+)\]/)
        @enemy.die_switch = $1.to_i
      end
      if @list[value].parameters[0].include?("[variable")
        @list[value].parameters[0].scan(/\[variable ([0.0-9.9]+)\]/)
        @enemy.die_variable = $1.to_i
      end
    end
  end
  def run_enemy_commands
    ers = @enemy.die_erase
    $game_map.enemies.delete(self)
    unless @enemy.die_localsw.nil?
      key = [$game_map.map_id,@id,Sapphire_Core::Local_Switch[@enemy.die_localsw]]
      $game_self_switches[key] = true
      $game_map.need_refresh = true
    end
    unless @enemy.die_variable.nil?
      $game_variables[@enemy.die_variable] += 1
      $game_map.need_refresh = true
    end
    unless @enemy.die_switch.nil?
      $game_switches[@enemy.die_switch] = true
      $game_map.need_refresh = true
    end
    @enemy = nil
    erase if ers
  end
  def move_type_toward_player
    move_toward_player if near_the_player?
  end
  def setup_page_settings
    kp_setup_page_settings
    setup_collision
    multiply_commands
  end
  def collision?(px,py)
    for event in $game_map.events.values
      if (event.px - px).abs <= event.cx && (event.py - py).abs <= event.cy
        next if event.through || event == self
        return true if event.priority_type == 1
      end
    end
    if @priority_type == 1
      return true if ($game_player.px - px).abs <= @cx && ($game_player.py - py).abs <= @cy
    end
    return false
  end
  def setup_collision
    @cx = Default_Collision_X
    @cy = Default_Collision_Y
    unless @list.nil?
      for value in 0...@list.size
        next if @list[value].code != 108 && @list[value].code != 408
        if @list[value].parameters[0].include?("[collision_x ")
          @list[value].parameters[0].scan(/\[collision_x ([0.0-9.9]+)\]/)
          @cx = $1.to_i
        end
        if @list[value].parameters[0].include?("[collision_y ")
          @list[value].parameters[0].scan(/\[collision_y ([0.0-9.9]+)\]/)
          @cy = $1.to_i
        end
      end
    end
  end
  def front_pixel_touch?(px,py)
    return if $game_map.interpreter.running?
    if @enemy.nil?
      if @trigger == 2 && ($game_player.px - px).abs <= @cx && ($game_player.py - py).abs <= @cy
        start if !jumping? && normal_priority?
      end
    else
      return if jumping? || @recover > 0 || @enemy.nature == 2 || @enemy.object
      attack if $game_map.sas_active && ($game_player.px - px).abs <= @cx && ($game_player.py - py).abs <= @cy
    end
  end
end

#-------------------------------------------------------------------------------
# * Game Interpreter
#-------------------------------------------------------------------------------

class Game_Interpreter
  def self_event
    return $game_map.events[@event_id]
  end
end

#-------------------------------------------------------------------------------
# * Sapphire Bitcore
#-------------------------------------------------------------------------------

module Sapphire_Bitcore
  def self.initialize
    @@buffer = {}
    for skill in load_data("Data/Skills.rvdata2")
      next if skill.nil? || skill.particle.nil?
      Sapphire_Bitcore.push(skill.particle)
    end
  end
  def self::[](key)
    return @@buffer[key]
  end
  def self.push(key)
    return if @@buffer.keys.include?(key)
    @@buffer[key] = Cache.particle(key)
  end
end

Sapphire_Bitcore.initialize

#-------------------------------------------------------------------------------
# * Sapphire Action System IV - Script End
#-------------------------------------------------------------------------------
