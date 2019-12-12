name: Node

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [10.x]
    steps:
    - uses: actions/checkout@v1
    # - name: install sshpass
    #   run: sudo apt-get install sshpass 
    - name: install Node.js
      uses: actions/setup-node@v1
      # with:
    #     node-version: ${{ matrix.node-version }}
    # - name: npm install, build
    #   run: |
    #     npm install 
    #     npm run build
    #  - name: scp aliyunEcs 
    #    run: sshpass -p "123456Zr" scp -r ./dist root@106.14.17.48:/root/
    - name: copy dir to remote server
        uses: appleboy/scp-action@master
        with:
          host: '106.14.17.48'  #${{ secrets.HOST }}
          username: 'root'  #${{ secrets.USERNAME }}
          source: "dist"
          target: 'root' #${{secrets.DIR}}
          key: '123456Zr' # ${{secrets.KEY}}
          rm: true