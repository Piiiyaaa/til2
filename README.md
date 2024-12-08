# til2(Today i learned)

こちらのリポジトリは学習用のリポジトリです。

class CatSimulator
  def initialize
    @kittens = ["kitten-A"]  # 最初の子猫
    @cats = []               # 大人の猫たち
    @births = {}            # 各子猫の誕生年を記録
  end

  def simulate(years)
    @births["kitten-A"] = 0  # 最初の子猫は0年目に誕生

    years.times do |year|
      year_num = year + 1
      
      # 成長: 子猫が2年経過して猫になる
      grow_kittens = []
      @kittens.each do |kitten|
        if @births[kitten] && (year_num - @births[kitten]) >= 2
          @cats << kitten.sub("kitten", "cat")
          grow_kittens << kitten
        end
      end
      grow_kittens.each { |k| @kittens.delete(k) }

      # 繁殖: 猫が新しい子猫を産む
      @cats.each do |cat|
        new_kitten = "kitten-#{(('A'.ord + @births.size).chr)}"
        @kittens << new_kitten
        @births[new_kitten] = year_num
      end
    end

    { cat: @cats.size, kitten: @kittens.size }
  end
end

