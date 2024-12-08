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


____



class TreeSimulator
  def initialize
    @seedlings = ["seedling-A"]  # 初期状態の苗
    @trees = []                 # 木のリスト
    @fruits = []                # 実のリスト
    @births = {}                # 苗の誕生年を記録
  end

  def simulate(years)
    # 初期苗の誕生年を記録
    @births["seedling-A"] = 0

    years.times do |year|
      year_num = year + 1

      # 苗が1年経過して木に成長
      grow_seedlings = []
      @seedlings.each do |seedling|
        if @births[seedling] && (year_num - @births[seedling]) >= 1
          @trees << seedling.sub("seedling", "tree")
          grow_seedlings << seedling
        end
      end
      grow_seedlings.each { |s| @seedlings.delete(s) }

      # 木が実を付ける
      @trees.each do |tree|
        @fruits << "fruit-#{(('A'.ord + @fruits.size).chr)}"
      end
    end

    # 結果を返す
    {
      seedling: @seedlings.size,
      tree: @trees.size,
      fruit: @fruits.size
    }
  end
end

# テスト実行用
years = 5
simulator = TreeSimulator.new
result = simulator.simulate(years)
puts result


