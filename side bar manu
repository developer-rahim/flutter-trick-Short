import 'package:active_ecommerce_flutter/data_model/message_response.dart';
import 'package:active_ecommerce_flutter/data_model/sub_category_model.dart';
import 'package:active_ecommerce_flutter/main.dart';
import 'package:active_ecommerce_flutter/my_theme.dart';
import 'package:active_ecommerce_flutter/screens/cart.dart';
import 'package:active_ecommerce_flutter/screens/category_products.dart';
import 'package:active_ecommerce_flutter/screens/filter.dart';
import 'package:active_ecommerce_flutter/screens/home.dart';
import 'package:active_ecommerce_flutter/screens/main.dart';
import 'package:active_ecommerce_flutter/screens/messenger_list.dart';
import 'package:active_ecommerce_flutter/screens/profile.dart';
import 'package:active_ecommerce_flutter/ui_sections/drawer.dart';
import 'package:flutter/material.dart';
import 'dart:convert';
import 'package:flutter_spinkit/flutter_spinkit.dart';
import 'package:http/http.dart' as http;

class CategoryList2 extends StatefulWidget {
  @override
  State<CategoryList2> createState() => _CategoryList2State();
}

class _CategoryList2State extends State<CategoryList2> {
  int selectedIndex = 0;
  var categorieslist = [];
  //var subCategories = [];
  var subCategories3 = [];
  PageController pageController = PageController();
  Future getCategories() async {
    try {
      var url = 'https://pk.tamampk.com/api/v2/categories';
      http.Response response = await http.get(Uri.parse(url));
      var data = jsonDecode(response.body)['data'];
      print('Adataeeeeeeee $data');
      setState(() {
        categorieslist = data;
      });
      return data;
    } catch (err) {
      print(err.toString());
    }
  }

  final GlobalKey<ScaffoldState> _scaffoldKey = new GlobalKey<ScaffoldState>();
  var categoryId = 1;
  var categoryId3 = 3;
  @override
  void initState() {
    // getSubCategories();
    //getSubCategories3();
    getCategories();
    // getSubCategories(id: 1);
    // TODO: implement initState
    super.initState();
  }

  @override
  Widget build(BuildContext context) {
    return SafeArea(
      child: Scaffold(
        key: _scaffoldKey,
        backgroundColor: Colors.white,
        drawer: MainDrawer(),
        appBar: buildAppBar(context),
        body: Row(
          children: [
            Container(
              width: 85,
              color: Colors.black.withOpacity(0.1),
              child: ListView.builder(
                  itemCount: categorieslist.length,
                  itemBuilder: (context, index) {
                    return GestureDetector(
                      onTap: () {
                        setState(() {
                          selectedIndex = index;
                          categoryId = categorieslist[index]['id'];
                          // getSubCategories(id: categoryId);
                          pageController.jumpToPage(index);
                        });
                        print('iD $categoryId');
                      },
                      child: Container(
                        child: Row(
                          children: [
                            // AnimationController(duration: Duration(milliseconds: 5))
                            // Padding(
                            //   padding: const EdgeInsets.only(left: 5),
                            //   child: AnimatedContainer(
                            //     duration: Duration(milliseconds: 500),
                            //     height: selectedIndex == index ? 100 : 0,
                            //     child: Container(
                            //       height: selectedIndex == index ? 150 : 0,
                            //       width: 5,
                            //       color: MyTheme.Grey_third,
                            //     ),
                            //   ),
                            // ),

                            Expanded(
                                child: Container(
                              width: 0,
                              color: selectedIndex == index
                                  ? Colors.white
                                  : Colors.transparent,
                              child: Padding(
                                padding: EdgeInsets.symmetric(
                                    vertical: 10, horizontal: 10),
                                child: Column(
                                  children: [
                                    Container(
                                      height: 50,
                                      child: ClipRRect(
                                          borderRadius:
                                              BorderRadius.circular(10),
                                          child: Image.network(
                                            categorieslist[index]['banner'],
                                            fit: BoxFit.fill,
                                            width: double.infinity,
                                          )),
                                    ),
                                    Text(
                                      categorieslist[index]['name'],
                                      style: TextStyle(color: Colors.black),
                                      // 'Tab title $index'
                                    ),
                                  ],
                                ),
                              ),
                            ))
                          ],
                        ),
                      ),
                    );
                  }),
            ),
            Expanded(
                child: PageView(
              controller: pageController,
              children: [
                //  for (int i = 1; i <= categorieslist.length; i++)

                // Container(child: Text('data1 $i')),

                Container(
                  child: Padding(
                    padding: const EdgeInsets.all(12.0),
                    child: FutureBuilder(
                      future: getSubCategories(categoryId.toString()),
                      builder: (context, snapshot) {
                        List<Data> data = snapshot.data;
                        print(data);
                        if (snapshot.hasData) {
                          return GridView.builder(
                              gridDelegate:
                                  SliverGridDelegateWithFixedCrossAxisCount(
                                      crossAxisCount: 3,
                                      childAspectRatio: 1.1,
                                      crossAxisSpacing: 25,
                                      mainAxisSpacing: 15),
                              itemCount: data.length,
                              itemBuilder: (BuildContext ctx, subindex) {
                                return GestureDetector(
                                  onTap: () {
                                    Navigator.push(context,
                                        MaterialPageRoute(builder: (context) {
                                      return CategoryProducts(
                                        category_id: data[subindex].id,
                                        category_name: data[subindex].name,
                                      );
                                    }));
                                  },
                                  child: Container(
                                    alignment: Alignment.center,
                                    child: Column(
                                      children: [
                                        Expanded(
                                          child: Container(
                                            // height: 50,
                                            child: ClipRRect(
                                                borderRadius:
                                                    BorderRadius.circular(10),
                                                child: Image.network(
                                                  data[subindex].banner,
                                                  fit: BoxFit.fill,
                                                  width: double.infinity,
                                                )),
                                          ),
                                        ),
                                        Text(
                                          data[subindex].name,
                                          style: TextStyle(color: Colors.black),
                                        ),
                                      ],
                                    ),
                                    decoration: BoxDecoration(
                                        // color: MyTheme.Grey_third,
                                        borderRadius:
                                            BorderRadius.circular(15)),
                                  ),
                                );
                              });
                        } else {
                          return Center(
                            child: Image.asset(
                              "assets/Loading_icon.gif",
                              fit: BoxFit.contain,
                            ),
                            //  SpinKitFadingCircle(
                            //   itemBuilder: (BuildContext context, int index) {
                            //     return DecoratedBox(
                            //       decoration: BoxDecoration(
                            //         color:
                            //             index.isEven ? Colors.red : Colors.green,
                            //       ),
                            //     );
                            //   },
                            // )
                          );
                        }
                      },
                    ),
                  ),
                ),
              ],
            ))
          ],
        ),
      ),
    );
  }

  Future getSubCategories(String id) async {
    try {
      var url = 'https://www.tamampk.com/api/v2/sub-categories/${id}';
      http.Response response = await http.get(Uri.parse(url));
      //var data = jsonDecode(response.body)['data'];
      final json = jsonDecode(response.body);
      SubCategory subCategory = SubCategory.fromJson(json);
      List<Data> data = subCategory.data;
      print('Subeeeeeeee $data');
      // setState(() {
      //   subCategories = data;
      // });
      return data;
    } catch (err) {
      print(err.toString());
    }
  }

  AppBar buildAppBar(BuildContext context) {
    return AppBar(
      backgroundColor: Colors.white,
      // centerTitle: true,
      actions: [
        IconButton(
          onPressed: () {
            Navigator.push(context, MaterialPageRoute(builder: (context) {
              return Filter();
            }));
          },
          icon: Icon(
            Icons.search,
            color: MyTheme.dark_grey,
            size: 27,
          ),
        ),
        SizedBox(
          width: 16,
        ),
        Container(
          margin: EdgeInsets.only(right: 16),
          //  color: Colors.amber,
          height: 20, width: 23,
          child: GestureDetector(
            onTap: () {
              Navigator.push(context, MaterialPageRoute(builder: (context) {
                return Cart(has_bottomnav: false);
              }));
            },
            child: Image.asset(
              "assets/cart.png",
              fit: BoxFit.contain,
            ),
          ),
        ),
        PopupMenuButton(
            // add icon, by default "3 dot" icon
            icon: Icon(
              Icons.more_vert,
              color: MyTheme.dark_grey,
            ),
            itemBuilder: (context) {
              return [
                PopupMenuItem<int>(
                  value: 0,
                  child: Text("Home"),
                ),
                PopupMenuItem<int>(
                  value: 1,
                  child: Text("Messages"),
                ),
                PopupMenuItem<int>(
                  value: 2,
                  child: Text("Profile"),
                ),
              ];
            },
            onSelected: (value) {
              if (value == 0) {
                Navigator.push(context, MaterialPageRoute(builder: (context) {
                  return Main();
                }));
              } else if (value == 1) {
                Navigator.push(context, MaterialPageRoute(builder: (context) {
                  return MessengerList();
                }));
              } else if (value == 2) {
                Navigator.push(context, MaterialPageRoute(builder: (context) {
                  return Profile();
                }));
              }
            }),
      ],
      leading: GestureDetector(
        child: Builder(
          builder: (context) => GestureDetector(
            onTap: () {
              _scaffoldKey.currentState.openDrawer();
            },
            child: Padding(
              padding:
                  const EdgeInsets.symmetric(vertical: 18.0, horizontal: 0.0),
              child: Container(
                child: Image.asset(
                  'assets/hamburger.png',
                  height: 16,
                  color: MyTheme.dark_grey,
                ),
              ),
            ),
          ),
        ),
      ),
      title: Text(
        'Categories',
        style: TextStyle(
          fontSize: 20,
          color: MyTheme.dark_grey,
        ),
      ),
      elevation: 0.0,
      titleSpacing: 0,
    );
  }
}
