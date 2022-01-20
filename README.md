# test-java-tanpa-PLSQL




package gov.dukcapil.web.apps.siakApp.siak.pengaturan.instansi;

import gov.dukcapil.web.apps.siakApp.SubVerticalSiakApp;
import gov.dukcapil.web.libs.helper.Dukcapil;
import io.vertx.core.MultiMap;
import io.vertx.core.Vertx;
import io.vertx.core.json.JsonArray;
import io.vertx.core.json.JsonObject;
import io.vertx.ext.web.Router;
import io.vertx.ext.web.RoutingContext;

public class Kategori extends SubVerticalSiakApp {
	
//	private static final String PKG_TAB_VIEW = "CALL SIAK_CONF.PKG_CONF_PINDAI.TAB_VIEW(?,?,?,?,?,?)";
	private static final String PKG_TAB_VIEW_MAIN = "CALL SIAK_CONF.PKG_CONF_PINDAI.TAB_VIEW_MAIN(?,?,?,?,?)";

	public Kategori(Vertx vertx) {
		super(vertx);
	}
	
	@Override
	public void getRouter(Router router) {
		router.route(Dukcapil.URL_TAB_VIEW_MAIN).handler(context -> {
			context.put(Dukcapil.REQ_STARTTIME, System.currentTimeMillis());
			tabViewMain(context);
		});
		
		router.route(Dukcapil.URL_SEARCH_LIST).handler(context -> {
			context.put(Dukcapil.REQ_STARTTIME, System.currentTimeMillis());
			searchList(context);
		});
		
		router.route(Dukcapil.URL_SEARCH_LIST_DATA).handler(context -> {
			context.put(Dukcapil.REQ_STARTTIME, System.currentTimeMillis());
			searchListData(context);
		});
		
	}
	
	private void tabViewMain(RoutingContext context) {
		final JsonObject principal = context.user().principal();
		final String authRuleAdd = "040102010101";
		
		final JsonArray pkgTabViewMainIn = new JsonArray();
		pkgTabViewMainIn.add(principal.getString(PRINCIPAL_USERNAME));
		pkgTabViewMainIn.add(authRuleAdd);
		
		final JsonArray pkgTabViewMainOut = new JsonArray();
		pkgTabViewMainOut.addNull();
		pkgTabViewMainOut.addNull();
		pkgTabViewMainOut.add(java.sql.Types.SMALLINT);
		pkgTabViewMainOut.add(java.sql.Types.VARCHAR);
		
		responseBody = new JsonObject();
		responseBody.put(Dukcapil.AUTH_RULE_ADD, Dukcapil.DUKCAPIL_VALUE_N);
		responseClientSuccess(context, responseBody);
		return;
		// siakLogger.info("{}\nparamIn: {}\nparamOut: {}", PKG_TAB_VIEW_MAIN, pkgTabViewMainIn, pkgTabViewMainOut);
//		dbService.callQuery(PKG_TAB_VIEW_MAIN, pkgTabViewMainIn, pkgTabViewMainOut, pkgTabViewMain -> {
//			if (pkgTabViewMain.succeeded()) {
//				final JsonArray pkgTabViewMainResult = pkgTabViewMain.result();
//				// siakLogger.info("{}\nResult: {}", PKG_TAB_VIEW_MAIN, pkgTabViewMainResult);
//				final int status = pkgTabViewMainResult.getInteger(2);
//				if (status != Dukcapil.RESP200) {
//					if (status != Dukcapil.RESP401) {
//						responseBody = new JsonObject();
//						responseBody.put(Dukcapil.RESP_MESSAGE, pkgTabViewMainResult.getString(3));
//						responseClientError(context, status, responseBody);
//						return;
//					}
//
//					responseBody = new JsonObject();
//					responseBody.put(Dukcapil.AUTH_RULE_ADD, Dukcapil.DUKCAPIL_VALUE_N);
//					responseClientSuccess(context, responseBody);
//					return;
//				}
//
//				responseBody = new JsonObject();
//				responseBody.put(Dukcapil.AUTH_RULE_ADD, Dukcapil.DUKCAPIL_VALUE_Y);
//				responseClientSuccess(context, responseBody);
//			} else {
//				siakLogger.error("Database service failed on {}", pkgTabViewMain.cause(), PKG_TAB_VIEW_MAIN);
//				responseBody = new JsonObject();
//				responseBody.put(Dukcapil.RESP_MESSAGE, DEFAULT_DB_EXCEPTION_MESSAGE);
//				responseClientError(context, responseBody);
//			}
//		});
	}
	
	private void searchList(RoutingContext context) {
		final JsonObject principal = context.user().principal();
		final String authRuleParentId = "04010301";
//		final String authRuleDetail = "0401030101";
//		final String authRuleEdit = "040102010103";
//		final String authRuleDelete = "040102010104";
//		final String authRuleAktifasi = "040102010105";
		
		final JsonArray pkgSearchListIn = new JsonArray();
		pkgSearchListIn.add(principal.getString(PRINCIPAL_USERNAME));
		pkgSearchListIn.add(authRuleParentId);
		
		final JsonArray pkgSearchListOut = new JsonArray();
		pkgSearchListOut.addNull();
		pkgSearchListOut.addNull();
		pkgSearchListOut.add(java.sql.Types.SMALLINT);
		pkgSearchListOut.add(java.sql.Types.VARCHAR);
		pkgSearchListOut.add(java.sql.Types.VARCHAR);
		
		responseBody = new JsonObject();
		responseBody.put(Dukcapil.AUTH_RULE_ADD, Dukcapil.DUKCAPIL_VALUE_N);
		responseClientSuccess(context, responseBody);
		return;
		
		// siakLogger.info("{}\nparamIn: {}\nparamOut: {}", PKG_SEARCH_LIST, pkgSearchListIn, pkgSearchListOut);
//		dbService.callQuery(PKG_SEARCH_LIST, pkgSearchListIn, pkgSearchListOut, pkgSearchList -> {
//			if (pkgSearchList.succeeded()) {
//				final JsonArray pkgSearchListResult = pkgSearchList.result();
//				// siakLogger.info("{}\nResult: {}", PKG_SEARCH_LIST, pkgSearchListResult);
//				final int status = pkgSearchListResult.getInteger(2);
//				if (status != Dukcapil.RESP200) {
//					responseBody = new JsonObject();
//					responseBody.put(Dukcapil.RESP_MESSAGE, pkgSearchListResult.getString(3));
//					if (status != Dukcapil.RESP401) {
//						responseClientError(context, status, responseBody);
//						return;
//					}
//					responseClientError(context, Dukcapil.RESP403, responseBody);
//					return;
//				}
//				
//				responseBody = new JsonObject();
//				responseBody.put(Dukcapil.AUTH_RULE_DETAIL, Dukcapil.DUKCAPIL_VALUE_N);
//				responseBody.put(Dukcapil.AUTH_RULE_EDIT, Dukcapil.DUKCAPIL_VALUE_N);
//				responseBody.put(Dukcapil.AUTH_RULE_DELETE, Dukcapil.DUKCAPIL_VALUE_N);
//				responseBody.put(Dukcapil.AUTH_RULE_AKTIFASI, Dukcapil.DUKCAPIL_VALUE_N);
//				
//				if (pkgSearchListResult.getString(4) != null) {
//					final JsonObject jsonTab = new JsonObject(pkgSearchListResult.getString(4));
//					if (!jsonTab.isEmpty()) {
//						final JsonArray detail = new JsonArray();
//						jsonTab.forEach(keyStr -> {
//							final JsonObject detailData = new JsonObject(keyStr.getValue().toString());
//							detail.add(detailData);
//							if (detailData.containsKey(authRuleDetail)) {
//								responseBody.put(Dukcapil.AUTH_RULE_DETAIL, Dukcapil.DUKCAPIL_VALUE_Y);
//							} else if (detailData.containsKey(authRuleEdit)) {
//								responseBody.put(Dukcapil.AUTH_RULE_EDIT, Dukcapil.DUKCAPIL_VALUE_Y);
//							} else if (detailData.containsKey(authRuleDelete)) {
//								responseBody.put(Dukcapil.AUTH_RULE_DELETE, Dukcapil.DUKCAPIL_VALUE_Y);
//							} else if (detailData.containsKey(authRuleAktifasi)) {
//								responseBody.put(Dukcapil.AUTH_RULE_AKTIFASI, Dukcapil.DUKCAPIL_VALUE_Y);
//							}
//						});
//					}
//				}
//				responseClientSuccess(context, responseBody);
//			} else {
//				siakLogger.error("Database service failed on {}", pkgSearchList.cause(), PKG_SEARCH_LIST);
//				responseBody = new JsonObject();
//				responseBody.put(Dukcapil.RESP_MESSAGE, DEFAULT_DB_EXCEPTION_MESSAGE);
//				responseClientError(context, responseBody);
//			}
//		});
	}
	
	private void searchListData(RoutingContext context) {
		final JsonObject principal = context.user().principal();
		final JsonObject requestBody = new JsonObject(context.getBodyAsString());
		final JsonObject jsonReqColumn = requestBody.getJsonObject(Dukcapil.KEY_REQ_TABLE);
		final JsonObject jsonWhere = new JsonObject();
		if (jsonReqColumn.getInteger("CARI_NO_PROP") > 0) {
			jsonWhere.put("NO_PROV", jsonReqColumn.getInteger("CARI_NO_PROP"));
		}
		
		if (jsonReqColumn.getInteger("CARI_NO_KAB") > 0) {
			jsonWhere.put("NO_KAB", jsonReqColumn.getInteger("CARI_NO_KAB"));
		}
		
		if (jsonReqColumn.containsKey("CARI_ID_COMP")) {
			if (jsonReqColumn.getString("CARI_ID_COMP").length() > 0) {
				if (jsonReqColumn.getString("CARI_ID_COMP").indexOf(",") != -1) {
					final String[] cariIdComp = jsonReqColumn.getString("CARI_ID_COMP").split(",");
					final JsonArray idComp = new JsonArray();
					for (final String id : cariIdComp) {
						idComp.add(String.valueOf(id.trim()));
					}
					jsonWhere.put("ID_COMP IN", idComp);
				} else {
					jsonWhere.put("ID_COMP", jsonReqColumn.getString("CARI_ID_COMP"));
				}
			}
		}
		
		if (jsonReqColumn.containsKey("CARI_IP")) {
			if (jsonReqColumn.getString("CARI_IP").length() > 0) {
				jsonWhere.put("IP_ADDRESS", jsonReqColumn.getString("CARI_IP"));
			}
		}
		
		String order = "NO_PROV ASC,NO_KAB ASC,DESCRIPTION ASC";
		if (requestBody.containsKey("order")) {
			order = requestBody.getString("order");
		}
		
		int page = 1;
		if (requestBody.containsKey("page")) {
			page = requestBody.getInteger("page");
		}
		
		final JsonArray pkgProcSearchListDataIn = new JsonArray();
		pkgProcSearchListDataIn.add(principal.getString(PRINCIPAL_USERNAME));
		pkgProcSearchListDataIn.add(jsonWhere.encode());
		pkgProcSearchListDataIn.add(page);
		pkgProcSearchListDataIn.add(order);
		
		final JsonArray pkgProcSearchListDataOut = new JsonArray();
		pkgProcSearchListDataOut.addNull();
		pkgProcSearchListDataOut.addNull();
		pkgProcSearchListDataOut.addNull();
		pkgProcSearchListDataOut.addNull();
		pkgProcSearchListDataOut.add(java.sql.Types.SMALLINT);
		pkgProcSearchListDataOut.add(java.sql.Types.VARCHAR);
		pkgProcSearchListDataOut.add(java.sql.Types.VARCHAR);
		
		responseBody = new JsonObject();
		responseBody.put(Dukcapil.AUTH_RULE_ADD, Dukcapil.DUKCAPIL_VALUE_N);
		responseClientSuccess(context, responseBody);
		return;

		// siakLogger.info("{}\nparamIn: {}\nparamOut: {}", PKG_PROC_SEARCH_LIST_DATA, pkgProcSearchListDataIn, pkgProcSearchListDataOut);
//		dbService.callQuery(PKG_PROC_SEARCH_LIST_DATA, pkgProcSearchListDataIn, pkgProcSearchListDataOut, pkgProcSearchListData -> {
//			if (pkgProcSearchListData.succeeded()) {
//				final JsonArray pkgProcSearchListDataResult = pkgProcSearchListData.result();
//				// siakLogger.info("{}\nResult: {}", PKG_PROC_SEARCH_LIST_DATA, pkgProcSearchListDataResult);
//				final int status = pkgProcSearchListDataResult.getInteger(4);
//				if (status != Dukcapil.RESP200) {
//					if (status != Dukcapil.RESP404) {
//						responseBody = new JsonObject();
//						responseBody.put(Dukcapil.RESP_MESSAGE, pkgProcSearchListDataResult.getString(5));
//						responseClientError(context, Dukcapil.RESP404, responseBody);
//						return;
//					}
//					responseBody = new JsonObject();
//					responseBody.put(Dukcapil.RESP_MESSAGE, Dukcapil.RESP404_MSG01);
//					responseClientError(context, Dukcapil.RESP404, responseBody);
//					return;
//				}
//				
//				responseBody = new JsonObject(pkgProcSearchListDataResult.getString(6));
//				responseBody.put(Dukcapil.KEY_REQ_TABLE, jsonReqColumn);
//				responseClientSuccess(context, responseBody);
//			} else {
//				siakLogger.error("Database service failed on {}", pkgProcSearchListData.cause(), PKG_PROC_SEARCH_LIST_DATA);
//				responseBody = new JsonObject();
//				responseBody.put(Dukcapil.RESP_MESSAGE, DEFAULT_DB_EXCEPTION_MESSAGE);
//				responseClientError(context, responseBody);
//			}
//		});
	}
}

contoh java tanpa db
